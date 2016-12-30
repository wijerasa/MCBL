
.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: Microbiome Analysis
   :synopsis: Microbiome Analysis
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>


.. highlight:: rest


**********************************************
Basic Microbiome Analysis
**********************************************

QIIME
----------------

.. Note::

   :Required OS: OS x or Linux. 
   :Software: `Qiime 1.9 <http://qiime.org/index.html>`_ 
   :Documentation: `Qiime Tutorial <http://qiime.org/tutorials/index.html>`_
   :Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

File Formats
~~~~~~~~~~~~~~~~~~~~~~~~~~

#. This section includes descrption of varies file formats, including Qiime scripts, and parameters files. Read more `here <http://qiime.org/documentation/index.html>`_

   - `Qiime Script index <http://qiime.org/scripts/index.html#qiime-script-index>`_
   - `Input Files <http://qiime.org/documentation/file_formats.html>`_
       - `Metadata mapping files <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_. Metadata mapping files  provide per-sample metadata. 

.. tip::

   #SampleID BarcodeSequence LinkerPrimerSequence Treatment DOB Description
   
   PC.354 AGCACGAGCCTA YATGCTGCCTCCCGTAGGAGT Control 20061218 Control_mouse__I.D._354
   PC.355 AACTCGTCGATG YATGCTGCCTCCCGTAGGAGT Control 20061218 Control_mouse__I.D._355
   PC.356 ACAGACCACTCA YATGCTGCCTCCCGTAGGAGT Control 20061126 Control_mouse__I.D._356
   PC.607 AACTGTGCGTAC YATGCTGCCTCCCGTAGGAGT Fast 20071112 Fasting_mouse__I.D._607
   PC.634 ACAGAGTCGGCT YATGCTGCCTCCCGTAGGAGT Fast 20080116 Fasting_mouse__I.D._634

- `Plink <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `Projection Alignment <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `Phylip <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `FASTA <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_, `more <http://en.wikipedia.org/wiki/FASTA_format>`_
- `Fastq <https://en.wikipedia.org/wiki/FASTQ_format>`_
- `Numerical Data <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `Phenotype Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `Trait Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `Covariate Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `Marker Values as Numerical Co-variates <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `Square Numerical Matrix <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `Table Report <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
- `TOPM (Tags on Physical Map) <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_

Files You Need to Have 
~~~~~~~~~~~~~~~~~~~~~~~~~~

Following files need to be created or present before you start the pipeline:

1. Sequencing data files (.fastq or .fastq.gz)

.. Note::
   
   Fastq files should rename as follows, `more on page 7 <https://bytebucket.org/tasseladmin/tassel-5-source/wiki/docs/TasselPipelineGBS.pdf>`_

   :FLOWCELL_LANE_fastq.gz: example: AL2P1XXX_2_fastq.gz 
   :FLOWCELL_s_LANE_fastq.gz:  example: AL2P1XXX_s_2_fastq.gz 
   :code_FLOWCELL_s_LANE_fastq.gz:   example: 00000000_AL2P1XXX_s_2_fastq.gz


.. code-block:: bash
      :linenos:

      #To rename original .fastq.gz file, 
      $ mv  AE_S1_L001_R1_001.fastq.gz AL2P1XXX_1_fastq.gz

   
2. GBSv2 Key File. Example `key file <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/Pipeline_Testing_key.txt>`_, `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/KeyFileExample>`_

3. Referance Genome.   


GBSv2 Pipeline Plugins
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :header: "Plugin", "Description"
   :widths: 10, 40

   GBSSeqToTagDBPlugin,Executed to pull distinct tags from the database and export them in the fastq format. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/GBSSeqToTagDBPlugin>`_
   TagExportToFastqPlugin,Retrieves distinct tags stored in the database and reformats them to a FASTQ file. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/TagExportToFastqPlugin>`_
   SAMToGBSdbPlugin,Used to identify SNPs from aligned tags using the GBS DB. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/SAMToGBSdbPlugin>`_
   DiscoverySNPCallerPluginV2,Takes a GBSv2 database file as input and identifies SNPs from the aligned tags. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/DiscoverySNPCallerPluginV2>`_
   SNPQualityProfilerPlugin,Scores all discovered SNPs for various coverage depth and genotypic statistics for a given set of taxa. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/SNPQualityProfilerPlugin>`_
   UpdateSNPPositionQualityPlugin,Reads a quality score file to obtain quality score data for positions stored in the snpposition table. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/SNPCutPosTagVerificationPlugin>`_
   SNPCutPosTagVerificationPlugin,Allows a user to specify a Cut or SNP position for which they would like data printed. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/SNPCutPosTagVerificationPlugin>`_
   GetTagSequenceFromDBPlugin,Takes an existing GBSv2 SQLite database file as input and returns a tab-delimited file containing a list of Tag Sequences stored in the specified database file. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/GetTagSequenceFromDBPlugin>`_
   ProductionSNPCallerPluginV2,Converts data from fastq and keyfile to genotypes then adds these to a genotype file in VCF or HDF5 format. `More <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/ProductionSNPCallerPluginV2>`_


GBSv2 Pipeline 
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Load Tassel 5.0 module 

.. code-block:: bash
   :linenos:

   $ module load Tassel/5.0

2. Useful commands

To check all the plugins available, type

.. code-block:: bash
   :linenos:

   $ run_pipeline.pl -Xmx200g -ListPlugins

To check all the parameters for given Plugin, *Ex: GBSSeqToTagDBPlugin*, type

.. code-block:: bash
   :linenos:

   $ run_pipeline.pl -fork1 -GBSSeqToTagDBPlugin   -endPlugin -runfork1

.. tip::
   
   Users are recommended to read more about GBS command line options in `here. Page 1-2 <https://bytebucket.org/tasseladmin/tassel-5-source/wiki/docs/TasselPipelineGBS.pdf>`_

3. Create necessary folders and copy your raw data (fastqs), reference file and key file to appropriate folder,


.. code-block:: bash
   :linenos:

   $ mkdir fastq ref key db tagsForAlign hd5

4. Commands for the pipeline

.. code-block:: bash
   :linenos:

   $ run_pipeline.pl -Xmx200g -fork1 -GBSSeqToTagDBPlugin -i fastq  -k key/Tomato_key.txt -e ApeKI -db db/Tomato.db  -kmerLength 85 -mnQS 20  -endPlugin -runfork1
   $ run_pipeline.pl -fork1 -TagExportToFastqPlugin  -db db/Tomato.db -o tagsForAlign/tagsForAlign.fa.gz -c 5  -endPlugin -runfork1
   $ cd ref
   $ bwa index -a is S_lycopersicum_chromosomes.2.50.fa
   $ cd ../
   $ bwa samse ref/S_lycopersicum_chromosomes.2.50.fa tagsForAlign/tagsForAlign.sai tagsForAlign/tagsForAlign.fa.gz > tagsForAlign/tagsForAlign.sam
   $ run_pipeline.pl -fork1 -SAMToGBSdbPlugin -i tagsForAlign/tagsForAlign.sam  -db db/Tomato.db  -aProp 0.0 -aLen 0 -endPlugin -runfork1
   $ run_pipeline.pl -fork1 -DiscoverySNPCallerPluginV2 -db db/Tomato.db  -sC "chr00" -eC "chr12" -mnLCov 0.1 -mnMAF 0.01  -endPlugin -runfork1
   $ run_pipeline.pl -fork1 -ProductionSNPCallerPluginV2 -db db/Tomato.db  -e ApeKI -i fastq -k key/Tomato_key2.txt  -kmerLength 85 -mnQS 20 -o hd5/HapMap_tomato.h5 -endPlugin -runfork1

Mothur
----------------

