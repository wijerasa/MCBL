
.. module:: fastq_qc
   :synopsis: fastq_qc
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>

.. highlight:: rest


Fastq adapter removal and QC
****************************

.. Note::

	:Required OS: OS x or Linux. Windows users, please contact `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_ 
	:Software: `Trimmomatic <http://www.usadellab.org/cms/?page=trimmomatic>`_
	:Purpose: This document provides instructions about how to remove adapters and filter low quality bases from a Fastq file
	:More: Read more about `Read trimming adapter removing  here: <http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf>`_ 
	:Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_


Load the software 
-----------------

.. Note::
	If you are runing this on MCBL *mcic-ender-svr* following command will load the software module to your environment.

.. code-block:: bash
	:linenos:

	$ module load Trimmomatic/3.2.2

then you can get the help how to run Trimmomatic,

.. code-block:: bash
	:linenos:

	$ java -jar $TRIMHOME/trimmomatic-0.33.jar


Files needed
------------

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


Code examples
-------------

*Single-end fastq files*

.. code-block:: bash
	:linenos:

	$java -jar $TRIMHOME/trimmomatic-0.33.jar SE -threads 12 s_1_1_sequence.txt.gz lane1_forward.fq.gz ILLUMINACLIP:$TRIMHOME/adapters/TruSeq3-SE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36

*Paired End Fastq Files*

.. code-block:: bash
	:linenos:

	$java -jar $TRIMHOME/trimmomatic-0.33.jar PE -threads 12 C8EC8ANXX_s2_1_illumina12index_1_SL143785.fastq.gz C8EC8ANXX_s2_2_illumina12index_1_SL143785.fastq.gz C8EC8ANXX_s2_1_Trimmed_1P.fastq.gz C8EC8ANXX_s2_1_Trimmed_1U.fastq.gz C8EC8ANXX_s2_2_Trimmed_1P.fastq.gz C8EC8ANXX_s2_2_Trimmed_1U.fastq.gz ILLUMINACLIP:$TRIMHOME/adapters/TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36


*Multiple fastq files*

.. tip::
	Assumption has been made that your data in "Raw_Data" folder

:Input Files:	C6EF7ANXX_s3_1_illumina12index_10_SL100996.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_19_SL100997.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_22_SL100998.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_25_SL100999.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_27_SL101000.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_3_SL100994.fastq.gz
				C6EF7ANXX_s3_1_illumina12index_5_SL100995.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_10_SL100996.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_19_SL100997.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_22_SL100998.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_25_SL100999.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_27_SL101000.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_3_SL100994.fastq.gz
				C6EF7ANXX_s3_2_illumina12index_5_SL100995.fastq.gz


These are paired-end fastq files. **e.g** *C6EF7ANXX_s3_1_illumina12index_10_SL100996.fastq.gz and C6EF7ANXX_s3_2_illumina12index_10_SL100996.fastq.gz* belongs to single sample.

:Adapter File: $TRIMHOME/adapters/TruSeq3-PE.fa (Make sure you change this accordingly)

:Output Files: Each paired-end read (**e.g** *C6EF7ANXX_s3_1_illumina12index_10_SL100996.fastq.gz and C6EF7ANXX_s3_2_illumina12index_10_SL100996.fastq.gz*) will give 4 outputs:

				* Q_trimmed_6EF7ANXX_s3_1_illumina12index_10_SL100996_1P.fastq.gz - for paired forwad reads
				* Q_trimmed_6EF7ANXX_s3_1_illumina12index_10_SL100996_1U.fastq.gz - for unpaired forward reads
				* Q_trimmed_6EF7ANXX_s3_2_illumina12index_10_SL100996_1P.fastq.gz - for paired reverse reads
				* Q_trimmed_6EF7ANXX_s3_2_illumina12index_10_SL100996_1U.fastq.gz - for unpaired reverse reads


.. code-block:: bash
	:linenos:

	$cd Raw_Data #make sure you change the folder name accordingly 
	$mkdir Trimmed_Data # Output will be saved here
	$files_1=(*_s3_1_*.fastq.gz);files_2=(*_s3_2_*.fastq.gz);sorted_files_1=($(printf "%s\n" "${files_1[@]}" | sort -u));sorted_files_2=($(printf "%s\n" "${files_2[@]}" | sort -u));for ((i=0; i<${#sorted_files_1[@]}; i+=1));do java -jar $TRIMHOME/trimmomatic-0.33.jar PE -threads 12  -trimlog Trimmed_Data/log-j3.stat -phred33   ${sorted_files_1[i]} ${sorted_files_2[i]} Trimmed_Data/Q_trimmed_${sorted_files_1[i]%%.*}_1P.fastq.gz Trimmed_Data/Q_trimmed_${sorted_files_1[i]%%.*}-U.fastq.gz Trimmed_Data/Q_trimmed_${sorted_files_2[i]%%.*}_1P.fastq.gz Trimmed_Data/Q_trimmed_${sorted_files_1[i]%%.*}-U.fastq.gz ILLUMINACLIP:$TRIMHOME/adapters/TruSeq3-PE:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:20 MINLEN:40  &>Trimmed_Data/stat.txt; done
