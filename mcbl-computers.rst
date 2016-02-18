
.. MCBL documentation master file, created by
   sphinx-quickstart on Wed Sep 23 17:00:18 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


.. module:: Computing Resources
   :synopsis: Servers at MCBL
.. moduleauthor:: Saranga Wijeratne<wijeratne.3@osu.edu>

.. highlight:: rest

.. figure:: Logo.png
   :align: right

**********************************************
MCBL Servers and Computing Resources
**********************************************

Servers Overview
----------------

.. csv-table::
   :header: "Server", "Processors","Cores","Memory", "Local Disk"
   :widths: 12, 38, 5,5,5

   mcic-ender-svr,four 2.40GHz ten-core Intel® Xeon processors E7-4870,40,1.0 TB,16TB
   mcic-ender-svr2,four 2.00GHz ten-core Intel® Xeon processors E7-4850,40,1.2 TB,10TB
   mcic-ent-srvr,two 2.67GHz six-core Intel® Xeon processors X7542,12, 250GB, 2.0TB

Workstations Overview
----------------------
.. csv-table::
   :header: "Workstation", "Processors","Cores","Memory", "Local Disk"
   :widths: 12, 38, 5,5,5

   mcic-galaxy-srvr,two 3.47GHz six-core Intel® Xeon processors X5690,12, 94 GB,2.6 TB
   mcic-mac-srvr,two 2.93GHz six-core Intel® Xeon processors X5670,12, 64 GB,4.0 TB

Software Overview
----------------------
Following bioinformatics software are availabe through MCBL.Some of the commercial software are available for MCBL users.
Please contact `Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_ for availability of the software.

Commercial Software
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :header: "Application", "Version","Description","Contact"
   :widths: 10, 12, 40,15

   CLCBio Workbench,8.5.1,A comprehensive and user-friendly analysis package for analyzing comparing and visualizing next generation sequencing data,`Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_
   Blast2GO Pro,Pro,A complete framework for functional annotation and analysis,`Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

Open Source Software
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :header: "Application", "Version","Description","Module Name"
   :widths: 10, 12, 40,10

   Bowtie,1.1.0/2-2.2.3,An ultrafast and memory-efficient tool for aligning sequencing reads to long reference sequences,Bowtie-<version>
   Cd-hit,4.6.1,A very widely used program for clustering and comparing protein or nucleotide sequences,cd-hit-v<version>
   Cutadapt,1.4.2/1.8.1,Removes adapter sequences from high-throughput sequencing data,Cutadapt/<version>
   Exonerate,2.2.0,A generic tool for pairwise sequence comparison,Exonerate/<version>
   Express,1.5.1,eXpress is a streaming tool for quantifying the abundances of a set of target sequences from sampled subsequences,express-<version>
   Fastqc,1.5.1,Aims to provide a simple way to do some quality control checks on raw sequence data coming from high throughput sequencing pipelines,Fastqc-<version>
   GenomeAnalysisTK,3.2-2,GATK tools for error modeling data compression and variant calling,GenomeAnalysisTK-<version>
   Maker,2.31.8,MAKER is a portable and easily configurable genome annotation pipeline.,Maker/<version>
   Mothur,1.33/1.35,Tool for analyzing 16S rRNA gene sequences.,Mothur-<version>
   Mummer,3.23,A system for rapidly aligning entire genomes whether in complete or draft form.,Mummer/<version>
   Pandaseq,2.8,A program to align Illumina reads optionally with PCR primers embedded in the sequence and reconstruct an overlapping sequence.,Pandaseq/<version>
   Qiime,1.8,A program for comparison and analysis of microbial communities primarily based on high-throughput amplicon sequencing data.,Qiime-<version>
   Rsem,1.2.16,A software package for estimating gene and isoform expression levels from RNA-Seq data.,rsem-<version>
   Samtools,0.1.19,Provides various utilities for manipulating alignments in the SAM format including sorting merging indexing and generating alignments in a per-position format,Samtools-<version>
   SNAP,0.1.19,A new sequence aligner that is 3-20x faster and just as accurate as existing tools like BWA-mem Bowtie2 and Novoalign,SNAP/<version>
   Trim-fastq,1.2.2,A Fastq quality trimmer.,Trim-fastq-<version>
   Trinity,r20140717,a novel method for the efficient and robust de novo reconstruction of transcriptomes from RNA-seq data.,Trinity


Python Modules
~~~~~~~~~~~~~~~~~~~~~~


   



