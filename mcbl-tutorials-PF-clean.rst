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

.. Note::
	If you are runing this on MCBL *mcic-ender-svr*, please skip the installation. Following command will load the software module to your environment.

.. code-block:: bash
	:linenos:

	$ module load fasq_filter/0.1


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

	Put your executables in ``~/bin`` or full path to executables in ``$PATH`` in the absence of ``sudo`` privilages.




	.. code-block:: bash

		#If your Samples.txt is saved under ~/Downloads
		$ cd ~/Downloads
