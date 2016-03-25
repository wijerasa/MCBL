
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
   - `Numerical Data <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
      - `Phenotype Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
      - `Trait Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
      - `Covariate Format <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
      - `Marker Values as Numerical Co-variates <https://bitbucket.org/tasseladmin/tassel-5-source/wiki/UserManual/Load/Load>`_
   
   
#. Use the Terminal and navigate to the location where Samples.txt is saved.

   .. code-block:: bash
      :linenos:

      #If your Samples.txt is saved under ~/Downloads
      $ cd ~/Downloads

#. On OS x, issue the following command to download your files:

   .. code-block:: bash
      :linenos:

      $ for f in $(cat Samples.txt ); do curl --progress-bar -O $f; done

#. On Linux, issue the following command to download your files,

   .. code-block:: bash
      :linenos:

      $ for f in $(cat Samples.txt ); do wget -v $f; done


Check *checksum*
~~~~~~~~~~~~~~~~~~~
To detect errors which may have been introduced during the downloading, you have to run checksum on your downloaded files.

#. Navigate to the location where you have downloaded your files.

   .. code-block:: bash
      :linenos:

      #If your files are saved under ~/Downloads
      $ cd ~/Downloads


#. Then, if you're on OS x Terminal, type in the following command:

   .. code-block:: bash
      :linenos:
      
      $ md5 * 

   .. parsed-literal::

      MD5 (C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz) = d41d8cd428f00b204e9800998ecf8427e
      MD5 (C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz) = d49d8cdf00j204e9800998ecf8427e
      MD5 (C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz) = d47d8cd98dfds0b204e9800998ecf8427e
      MD5 (C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz) = d42d8cd98f00bdfse9800998ecf8427e

   
   If you're on Linux terminal, type in the following commmand:

   .. code-block:: bash
      :linenos:
      
      $ md5sum *

   .. parsed-literal::

      d41d8cd428f00b204e9800998ecf8427e   C6V7FANXX_s3_0_TruseqHTDual_D703-TruseqHTDual_D501_SL104549.fastq.gz
      d49d8cdf00j204e9800998ecf8427ed56   C6V7FANXX_s5_0_TruseqHTDual_D709-TruseqHTDual_D506_SL104602.fastq.gz
      d47d8cd98dfds0b204e9800998ecf8427e  C6V7FANXX_s8_0_TruseqHTDual_D705-TruseqHTDual_D501_SL104565.fastq.gz
      d47d8cd98dfds0b204e9800998ecf8427e  C6V7FANXX_s8_0_TruseqHTDual_D712-TruseqHTDual_D508_SL104628.fastq.gz


.. tip::
   
   Match these checksum values with the values provided in the Excelsheet. For any samples with mismatching checksum, you have to re-download the samples.
