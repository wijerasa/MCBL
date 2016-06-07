.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: Illumina Quality Filtering and Adapter Removing
   :synopsis: Quality Assesment
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>


.. highlight:: rest


**********************************************
 Adapter Removing and Quality Filtering
**********************************************

.. Note::

	:Required OS: OS x or Linux. Windows users, please contact `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_ 
	:Software: `Trimmomatic <http://www.usadellab.org/cms/?page=trimmomatic>`_
	:Purpose: This document provides instructions about how to remove adapters and filter low quality reads from a Fastq file
	:More: Read more about `Read trimming adapter removing  here: <http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf>`_ 
	:Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

Load the Software 
--------

.. Note::
	If you are runing this on MCBL *mcic-ender-svr* following command will load the software module to your environment.

.. code-block:: bash
	:linenos:

	$ module load Trimmomatic/3.2.2

then you can get the help how to run Trimmomatic,

.. code-block:: bash
	:linenos:

	$ java -jar $TRIMHOME/trimmomatic-0.33.jar

File Needed
--------

:Input Files: In put files should be in fastq format/compressed fastq( .fq, .fastq, .fq.gz, .fastq.gz). Read `Introduction <http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf>`_ 
				e.g :C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq, C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq.gz, s_1_1_sequence.txt.gz lane1_forward.fq.gz 
:Adapter File:	Currently, following Adapter sequence files are hosted in MCBL server.
			  	
			  	* TruSeq2-PE.fa  
			  	* TruSeq2-SE.fa  
				* TruSeq3-PE.fa  
				* TruSeq3-SE.fa
				* NexteraPE-PE.fa

.. warning::

	If you want to make your own adapter sequence file, please read the `The Adapter Fasta section and Making cutome clipping files here <http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf>`_ before you make your Adapter sequence file.


Code Examples
----------

*Single End Fastq Files*

.. code-block:: bash
	:linenos:

	$ java -jar $TRIMHOME/trimmomatic-0.33.jar SE -threads 12 s_1_1_sequence.txt.gz lane1_forward.fq.gz ILLUMINACLIP:$TRIMHOME/adapters/TruSeq3-SE:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

*Paired End Fastq Files*

.. code-block:: bash
	:linenos:

	$ java -jar $TRIMHOME/trimmomatic-0.33.jar PE -threads 12 C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq.gz C8EC8ANXX_s2_2_illumina12index_1_SL143785.fastq.gz C8EC8ANXX_s2_1_Trimmed_1P.fastq.gz C8EC8ANXX_s2_1_Trimmed_1U.fastq.gz C8EC8ANXX_s2_2_Trimmed_1P.fastq.gz C8EC8ANXX_s2_2_Trimmed_1U.fastq.gz ILLUMINACLIP:$TRIMHOME/adapters/TruSeq3-SE:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36



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

      $ for f in $(cat Fastq_filenames.txt); do zcat $f | fastq_illumina_filter -vvN | gzip > ${f%.*.fastq.gz}.filtered.fastq.gz;done







