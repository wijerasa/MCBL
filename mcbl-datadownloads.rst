
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

	**Required Operating System:**
		OS x or Linux. Windows users, please contact `Maria Elena Hernandez-Gonzalez <mailto:hernandez-gonzal.2@osu.edu>`_ 

	**Software:**
		wget/curl

#. Create a Sample.txt file with your sample links(as provided in the Excel sheet) as follows:

.. code-block:: bash
 	#Content of the Sample.txt

	http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz
	http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
	http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
	http://mysample.download.org/dl/d4/Meulia/myprojectnumber/data_150522/C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz

#. Navigate to the location where Sample.txt is saved.

.. code-block:: bash
	#If your Sample.txt is saved under ~/Downloads
	$ cd ~/Downloads



   



