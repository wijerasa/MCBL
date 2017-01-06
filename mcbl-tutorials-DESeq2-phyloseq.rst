.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: DESeq2-phyloseq 
   :synopsis: DESeq2 phyloseq
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>


.. highlight:: rest

.. figure:: Logo.png
   :align: right

**********************************************
DESeq2 with phyloseq
**********************************************

.. Note::

	:Required OS: OS x or Linux. 
	:Software: R, phyloseq R library
	:Purpose: This document provides instructions about how to find differentially abundant OTUs for Microbiome Data
	:More: Read more about `phyloseq DEseq2: <http://joey711.github.io/phyloseq-extensions/DESeq2.html>`_ and `here <https://joey711.github.io/phyloseq/>`_
	:Author: This document is created by `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

Software Installation
--------

.. Note::
	If you are runing this on MCBL *mcic-sel019-d*, please skip the installation. Following command in R-Studio will load the software module to your environment.

.. code-block:: r
	:linenos:

	> library("phyloseq"); packageVersion("phyloseq")

Version::
    
    [1] ‘1.16.2’

On your own server,

.. code-block:: r
	:linenos:

	> source('http://bioconductor.org/biocLite.R')
	> biocLite('phyloseq')


Import data with phyloseq
--------

For this step you need Biom and mapping  file generated from Qiime pipeline.

:Input Biom File: otu_table_mc10_w_tax.biom
:Qiime Mapping File: mapping.txt
:Output File: DESeq2_Out

Copy all the input files to your "Working Directory" before you execute following commands.

.. code-block:: r
	:linenos:

	> biom_file<-"otu_table_mc10_w_tax.biom"
	> mapping_file<-"mapping.txt"
	> biom_otu_tax<-import_biom(biom_file) #Importing biomfile with phyloseq
	> mapping_file<-import_qiime_sample_data(mapping_file)  #Importing mapping file with phyloseq
	> merged_mapping_biom<-merge_phyloseq(biom_otu_tax,mapping_file) #Merging Biom and mapping file with phyloseq
	> colnames(tax_table(merged_mapping_biom))<-c("kingdom", "Phylum","Class", "Order", "Family", "Genus", "species") #Setting headings in the taxa table
	
.. code-block:: r
	:linenos:

	> merged_mapping_biom

Merged mapping and Biom output::

    phyloseq-class experiment-level object
    otu_table()   OTU Table:         [ 315 taxa and 9 samples ]
    sample_data() Sample Data:       [ 9 samples by 8 sample variables ]
    tax_table()   Taxonomy Table:    [ 315 taxa by 7 taxonomic ranks ]
 
.. code-block:: r
	:linenos:

    > head(mapping_file)

Mapping file should be looked like this::

	Sample Data:        [6 samples by 8 sample variables]:
	        X.SampleID BarcodeSequence LinkerPrimerSequence InputFileName Treatment         Tissue Time   Coding
	Samp.82    Samp.82              NA                   NA S_41_P2.fasta       Def    Rectal swab PCD0 D_PCD0_C
	Samp.83    Samp.83              NA                   NA S_41_P3.fasta       Def    Rectal swab PCD0 D_PCD0_C
	Samp.84    Samp.84              NA                   NA S_42_P2.fasta       Suf    Rectal swab PCD0 S_PCD0_C
	Samp.85    Samp.85              NA                   NA S_42_P3.fasta       Suf    Rectal swab PCD0 S_PCD0_C
	S272          S272              NA                   NA    S272.fasta       Suf Rectal swab NC PCD0 S_PCD0_C
	S273          S273              NA                   NA    S273.fasta       Suf Rectal swab NC PCD0 S_PCD0_C

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







