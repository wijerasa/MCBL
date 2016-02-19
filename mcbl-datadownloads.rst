
.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: Data Downloading
   :synopsis: Data Download
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>



.. figure:: Logo.png
   :align: right

**********************************************
Data Downloading from Cloud Services
**********************************************

Downloading from hudsonalpha.org
----------------

.. Note::

	:Required OS: OS x or Linux. Windows users, please contact `Maria Elena Hernandez-Gonzalez <mailto:hernandez-gonzal.2@osu.edu>`_ 

	:Software: wget/curl
         Terminal emulator:
            - Terminal (OS x)
            - Genome Terminal or Other Emulator (Linux)

#. Create a Samples.txt file with your sample links(the links are provided in the Excelsheet) as follows:

   .. parsed-literal::

	 	#Content of the Samples.txt
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
		http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz

#. Use the Terminal and navigate to the location where Samples.txt is saved.

	.. code-block:: bash

		#If your Samples.txt is saved under ~/Downloads
		$ cd ~/Downloads

#. On OS x, issue the following command to download your files:

	.. code-block:: bash

		$ for f in $(cat Samples.txt ); do curl --progress-bar -O $f; done

#. On Linux, issue the following command to download your files,

	.. code-block:: bash

		$ for f in $(cat Samples.txt ); do wget -v $f; done


Check *checksum*
~~~~~~~~~~~~~~~~~~~
To detect errors which may have been introduced during the downloading, you have to run checksum on your downloaded files.

#. Navigate to the location where you have downloaded your files.

   .. code-block:: bash

         #If your files are saved under ~/Downloads
         $ cd ~/Downloads


#. Then, if your on OS x Terminal, type in the following command:

   .. code-block:: bash
      
      $ md5 * 

   .. parsed-literal::

      MD5 (C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz) = d41d8cd428f00b204e9800998ecf8427e
      MD5 (C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz) = d49d8cdf00j204e9800998ecf8427e
      MD5 (C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz) = d47d8cd98dfds0b204e9800998ecf8427e
      MD5 (C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz) = d42d8cd98f00bdfse9800998ecf8427e

   
   If your on Linux terminal, type in the following commmand:

   .. code-block:: bash
      
      $ md5sum *

   .. parsed-literal::

      d41d8cd428f00b204e9800998ecf8427e   C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
      d49d8cdf00j204e9800998ecf8427ed56   C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
      d47d8cd98dfds0b204e9800998ecf8427e  C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz
      d47d8cd98dfds0b204e9800998ecf8427e  C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz


.. tip::
   
   Match these checksum values with the values provided in the Excelsheet. For any samples with mismatching checksum, you have to re-download the samples.
