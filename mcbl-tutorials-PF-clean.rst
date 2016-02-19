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
	:Purpose: This document provides instructions how to remove Passing Filter (PF) failed reads from a Fastq file
	:More: Read more about `PF here: <http://support.illumina.com/help/SequencingAnalysisWorkflow/Content/Vault/Informatics/Sequencing_Analysis/CASAVA/swSEQ_mCA_PercentageofClustersP.htm/>`_ and `here <http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/>`_
	:Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

Software Installation
--------

.. warning::

	If you dont have administrator privilages on the machine, you wouldn't be able run ``sudo`` (last command in the following code block) commands. 
	

.. code-block:: bash

	$ wget http://cancan.cshl.edu/labmembers/gordon/fastq_illumina_filter/fastq_illumina_filter-0.1.tar.gz
	$ tar -xzf fastq_illumina_filter-0.1.tar.gz
	$ cd fastq_illumina_filter-0.1
	$ make
	$ sudo cp fastq_illumina_filter /usr/local/bin


   .. parsed-literal::

		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz

#. Use the Terminal and navigate to the location where Samples.txt is saved.

	.. code-block:: bash

		#If your Samples.txt is saved under ~/Downloads
		$ cd ~/Downloads
