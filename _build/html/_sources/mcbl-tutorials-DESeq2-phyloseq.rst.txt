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
	If you are runing this on MCBL *mcic-sel019-d*, please skip the installation. The following command in R-Studio will load the software module to your environment.

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

	Sample Data:        [40 samples by 7 sample variables]:
    X.SampleID BarcodeSequence LinkerPrimerSequence InputFileName IncubationDate Treatment Description
	S1          S1              NA                   NA      S1.fasta              0        CO         CO1
	S2          S2              NA                   NA      S2.fasta              0        CO         CO2
	S3          S3              NA                   NA      S3.fasta              0        CO         CO3
	S4          S4              NA                   NA      S4.fasta             15        CO         CO4
	S5          S5              NA                   NA      S5.fasta             15        CO         CO5
	S6          S6              NA                   NA      S6.fasta             15        CO         CO6
	S7          S7              NA                   NA      S7.fasta             30        CO         CO7
	S23        S23              NA                   NA     S23.fasta             15        RE        RE22
	S24        S24              NA                   NA     S24.fasta             15        RE        RE23
	S25        S25              NA                   NA     S25.fasta             15        RE        RE24
	S26        S26              NA                   NA     S26.fasta             30        RE        RE25
	S27        S27              NA                   NA     S27.fasta             30        RE        RE26
	S28        S28              NA                   NA     S28.fasta             30        RE        RE27
	S29        S29              NA                   NA     S29.fasta             45        RE        RE28


To remove taxonomy level tags assigned to each level (k__, p__, etc..) issue the following codes:

.. code-block:: r
	:linenos:

	tax_table( merged_mapping_biom)<-gsub("k__([[:alpha:]])","\\1",tax_table( merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("p__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("c__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("o__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("f__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("g__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("s__([[:alpha:]])","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("p__(\\[)","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("c__(\\[)","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("o__(\\[)","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("f__(\\[)","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("g__(\\[)","\\1",tax_table(merged_mapping_biom))
	tax_table(merged_mapping_biom)<-gsub("s__(\\[)","\\1",tax_table(merged_mapping_biom))



Differential Abundance OTU call
------

:Input File: merged_mapping_biom
:Output Files: DESeq2_Out.txt

#. Load the DESeq2 into your R enviornment:

   .. code-block:: r
      :linenos:

      library("DESeq2")
      packageVersion("DESeq2")


   .. parsed-literal::

	 	[1] ‘1.12.4’


#. Assign DESeq2 output name and padj-cutoff 

   .. code-block:: r
      :linenos:

      filename_out<-"DESeq2_Out.txt"
      alpha<-0.01

#. *phyloseq_to_deseq2* function in the following lines converts phyloseq-format microbiom data (i.e merged_mapping_biom) into a *DESeqDataSet* with dispersion estimated, using experimental design formula (i.e ~ Treatment). 

   .. code-block:: r
      :linenos:

      diagdds <- phyloseq_to_deseq2(merged_mapping_biom, ~ Treatment)
      diagdds <- DESeq(diagdds, test="Wald", fitType="parametric")

   .. parsed-literal::

	 	## estimating size factors
		## estimating dispersions
		## gene-wise dispersion estimates
		## mean-dispersion relationship
		## final dispersion estimates
		## fitting model and testing


   .. warning::
	If you are getting the following error, please execute the code block below. `More... <https://github.com/joey711/phyloseq/issues/387>`_

	.. parsed-literal::

	   *Error in estimateSizeFactorsForMatrix(counts(object), locfunc, geoMeans = geoMeans) : every gene contains at least one zero, cannot compute log geometric means*
	   *Calls: estimateSizeFactors ... estimateSizeFactors -> .local -> estimateSizeFactorsForMatrix*


   .. code-block:: r
      :linenos:

      gm_mean = function(x, na.rm=TRUE){ exp(sum(log(x[x > 0]), na.rm=na.rm) / length(x))}
      geoMeans = apply(counts(diagdds), 1, gm_mean)
      diagdds = estimateSizeFactors(diagdds, geoMeans = geoMeans)
      diagdds = DESeq(diagdds, test="Wald", fitType="parametric")

#. The ``results`` function creats a table of results. Then the ``res`` table is filtered by ``padj < alpha``.

   .. code-block:: r
      :linenos:

      res = results(diagdds, cooksCutoff = FALSE)
      sigtab = res[which(res$padj < alpha), ]
      sigtab = cbind(as(sigtab, "data.frame"), as(tax_table(merged_mapping_biom)[rownames(sigtab), ], "matrix")) #Bind taxanomic information to final results table.
      write.csv(sigtab, as.character(filename_out)) #Writing `sigtab` to 








