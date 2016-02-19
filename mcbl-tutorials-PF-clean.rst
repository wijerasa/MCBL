.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: Illumina PF 
   :synopsis: Data Filtering Illumina
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>



.. figure:: Logo.png
   :align: right

**********************************************
Filter a Fastq File (CASAVA generated)
**********************************************

.. Note::

	:Required OS: OS x or Linux. Windows users, please contact `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_ 
	:Software: `Illumina CASAVA-1.8 FASTQ Filter <http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/>`_
	:Purpose: This document provides instructions about how to remove Passing Filter (PF) failed reads from a Fastq file
	:More: Read more about `PF here: <http://support.illumina.com/help/SequencingAnalysisWorkflow/Content/Vault/Informatics/Sequencing_Analysis/CASAVA/swSEQ_mCA_PercentageofClustersP.htm>`_ and `here <http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/>`_
	:Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

Software Installation
--------

.. Note::
	If you are runing this on MCBL *mcic-ender-svr*, please skip the installation. Following command will load the software module to your environment.

.. code-block:: bash
	:linenos:

	$ module load fasq_filter/0.1

On your own server,

.. warning::

	If you don't have administrator privilages on the machine, you wouldn't be able run ``sudo`` (last command in the following code block) commands. 
	


.. code-block:: bash
	:linenos:

	$ wget http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/fastq_illumina_filter-0.1.tar.gz
	$ tar -xzf fastq_illumina_filter-0.1.tar.gz
	$ cd fastq_illumina_filter-0.1
	$ make
	$ sudo cp fastq_illumina_filter /usr/local/bin



.. tip::

	Put your executables in ``~/bin`` or full-path to executables in ``$PATH`` in the absence of ``sudo`` privilages.

Filter a Fastq
--------

:Input File: C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq.gz
:Output File: C8EC8ANXX_s2_1_illumina12index_1_SL143785.filtered.fastq.gz

.. code-block:: bash
	:linenos:

	$ zcat C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq.gz | fastq_illumina_filter -vvN | gzip > C8EC8ANXX_s2_1_illumina12index_1_SL143785.filtered.fastq.gz

Filter Multiple Fastqs
-----

:Input File: Fastq_filenames.txt
:Output Files: Individual Fastq files

#. Create a Fastq_filenames.txt file with your Fastq filenames in seperate lines as follows:

   .. parsed-literal::

	 	#Content of the Samples.txt
	 	C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz
		C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
		C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
		C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz

#. Save the above file in the same folder with your Fastq files.

#. Use the Terminal and navigate to the location where Fastq_filenames.txt is saved.

   .. code-block:: bash
      :linenos:

      #If your Fastq_filenames.txt is saved under ~/Downloads
      $ cd ~/Downloads

#. Type in the following command to filter Fastqs in the Fastq_filenames.txt.

   .. code-block:: bash
      :linenos:

      $for f in $(cat Fastq_filenames.txt); do zcat $f | fastq_illumina_filter -vvN | gzip > {f%.*.fastq.gz}.filtered.fastq.gz;done







