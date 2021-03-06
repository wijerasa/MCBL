
.. module:: Microbiome
   :synopsis: Microbiome Analysis
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>

.. highlight:: rest


A basic microbiome analysis
***************************


QIIME
-----

.. Note::

   :Required OS: OS x or Linux
   :Software: `Qiime 1.9 <http://qiime.org/index.html>`_ 
   :Documentation: `Qiime tutorial <http://qiime.org/tutorials/index.html>`_
   :Author: This document was created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

File formats
~~~~~~~~~~~~

This section includes descrption of varies file formats, including Qiime scripts, and parameters files. Read more `here <http://qiime.org/documentation/index.html>`_

   **Qiime Script index:** `Index of all the scripts used in Qiime. <http://qiime.org/scripts/index.html#qiime-script-index>`_

   **Metadata mapping files:** Metadata mapping files  provide per-sample metadata.

.. tip::

   A metadata mapping file example is given `here <http://qiime.org/documentation/file_formats.html#mapping-file-overview>`_. Read the section carefully.
   If you are planning to create the mapping file by hand, read `this section. <http://qiime.org/documentation/file_formats.html#generating-a-mapping-file-by-hand>`_

   **Biom file:** OTU observation file. Read more `here <http://qiime.org/documentation/file_formats.html#biom-table-e-g-otu-table>`_.


Download the files
~~~~~~~~~~~~~~~~~~   

For this tutorial, we will use Mothur tutorial data from `Schloss Wiki <https://www.mothur.org/wiki/MiSeq_SOP>`_.
These data are 16s rRRNA Amplicons sequenced with Illumina MiSeq.

**1. Create folders**

Make a new directory ``MCICQiime`` and then `cd` to move into the dirctory. 

   .. code-block:: bash
      :linenos:

      $ mkdir  MCICQiime
      $ cd MCICQiime

**2. Download data**

Download data from `Schloss Wiki <https://www.mothur.org/wiki/MiSeq_SOP>`_

For this tutorial download only dataset shown in the image below (i.e Example data from Scholoss lab).

.. image:: img/qiime-data-scholos.png
   :width: 100%

Inside the ``MCICQiime`` dir, issue the following command to get the data.
The data has been zipped, and we will use ``unzip -j`` to extract all the files to same directory we are in right now.

   .. code-block:: bash
      :linenos:
      
      $ wget http://www.mothur.org/w/images/d/d6/MiSeqSOPData.zip  
      $ unzip -j  MiSeqSOPData.zip

Rename the files for downstream analyses:

   .. code-block:: bash
         :linenos:
         
         $ for f in *.fastq; do mv $f  ${f%%_L*}.fastq;done 

And explanation of the preceding commands:

- ``for f in *.fastq;`` reads any file that ends with `.fastq`, one at a time.
- ``do`` starts the body of the `for` loop.
- ``mv $f do mv $f  ${f%%_L*}.fastq;`` rename $f  (i.e F3D0_S188_L001_R1_001.fastq) to ${f%%_L*}.fastq (i.e F3D0_S188.fastq)
- ``done`` finishes the loop.

   
**3. An explanation of the data**

The files and experiment are described in the `Schloss Wiki <https://www.mothur.org/wiki/MiSeq_SOP>`_.

      Because of the large size of the original dataset (3.9 GB) we are giving you 21 of the 362 pairs of fastq files.
      For example, you will see two files: ``F3D0_S188_L001_R1_001.fastq`` and ``F3D0_S188_L001_R2_001.fastq``.
      These two files correspond to Female 3 on Day 0 (i.e. the day of weaning).
      The first and all those with R1 correspond to read 1 while the second and all those with R2 correspond to the second or reverse read.
      These sequences are 250 bp and overlap in the V4 region of the 16S rRNA gene; this region is about 253 bp long. So looking at the files
      in the ``MiSeq_SOP`` folder that you've downloaded you will see 22 fastq files representing 10 time points from Female 3 and 1 mock community.
      You will also see ``HMP_MOCK.v35.fasta`` which contains the sequences used in the mock community that we sequenced in fasta format.


GBSv2 pipeline plugins
~~~~~~~~~~~~~~~~~~~~~~

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


GBSv2 pipeline 
~~~~~~~~~~~~~~

**1. Load the Tassel 5.0 module**

.. code-block:: bash
   :linenos:

   $ module load Tassel/5.0

**2. Useful commands**

To check all the available plugins, type:

.. code-block:: bash
   :linenos:

   $ run_pipeline.pl -Xmx200g -ListPlugins

To check all the parameters for a given plugin, e.g. ``GBSSeqToTagDBPlugin``, type:

.. code-block:: bash
   :linenos:

   $ run_pipeline.pl -fork1 -GBSSeqToTagDBPlugin   -endPlugin -runfork1

.. tip::
   
   Users are recommended to read more about GBS command line options `here. Page 1-2 <https://bytebucket.org/tasseladmin/tassel-5-source/wiki/docs/TasselPipelineGBS.pdf>`_


**3. File preparation**

Create necessary folders and copy your raw data (fastqs), reference file and key file to appropriate folder:

.. code-block:: bash
   :linenos:

   $ mkdir fastq ref key db tagsForAlign hd5

**4. Commands for the pipeline**

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

