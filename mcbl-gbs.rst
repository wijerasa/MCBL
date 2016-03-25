
.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: GBS analysis
   :synopsis: GBS analysis
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>


.. highlight:: rest


**********************************************
Genotyping by Sequencing (GBS) pipeline documentation
**********************************************

.. Note::

   :Required OS: OS x or Linux. 
   :Software: `Tassel 5 <http://www.maizegenetics.net/#!tassel/c17q9>`_ 
   :Documentation: `Tassel 5.0 Wiki <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Home>`_
   :Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

File Formats
----------------

#. File formats that will be using in this analysis:

   - `HDF5 <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `VCF <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   - `Hapmap <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
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
----------------

Following files need to be created before you start the pipeline:

#. Sequencing data files (.fastq or .fastq.gz)

.. Note::
   
   Fastq files should rename as follows, `more on page 7 <https://bytebucket.org/tasseladmin/tassel-5-source/wiki/docs/TasselPipelineGBS.pdf>`_

   :FLOWCELL_LANE_fastq.gz: example: AL2P1XXX_2_fastq.gz 
   :FLOWCELL_s_LANE_fastq.gz:  example: AL2P1XXX_s_2_fastq.gz 
   :code_FLOWCELL_s_LANE_fastq.gz:   example: 00000000_AL2P1XXX_s_2_fastq.gz


.. code-block:: bash
      :linenos:

      #To rename original .fastq.gz file, 
      $ mv  AE_S1_L001_R1_001.fastq.gz AL2P1XXX_1_fastq.gz

   
#. GBSv2 Key File. Example `key file <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/Pipeline_Testing_key.txt>`_, `more <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/KeyFileExample>`_

   


GBSv2 Pipeline Plugins
----------------

.. csv-table::
   :header: "Plugin", "Description"
   :widths: 10, 40

   GBSSeqToTagDBPlugin, executed to pull distinct tags from the database and export them in the fastq format, more <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/GBSSeqToTagDBPlugin>`_
   TagExportToFastqPlugin, retrieves distinct tags stored in the database and reformats them to a FASTQ file, `more <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/Tassel5GBSv2Pipeline/TagExportToFastqPlugin>`_
   `Jody Whittier <whittier.2@osu.edu>`_,MCBL payments


.. tip::
   
   Match these checksum values with the values provided in the Excelsheet. For any samples with mismatching checksum, you have to re-download the samples.
