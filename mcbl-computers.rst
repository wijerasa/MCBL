
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
3. MCBL Servers and Computing Resources
**********************************************

3.1 Servers Overview
----------------

.. csv-table::
   :header: "Server", "Processors","Cores","Memory", "Local Disk"
   :widths: 12, 38, 5,5,5

   mcic-ender-svr,four 2.40GHz ten-core Intel® Xeon processors E7-4870,40,1.0 TB,16TB
   mcic-ender-svr2,four 2.00GHz ten-core Intel® Xeon processors E7-4850,40,1.2 TB,10TB
   mcic-ent-srvr,two 2.67GHz six-core Intel® Xeon processors X7542,12, 250GB, 2.0TB

3.2 Workstations Overview
----------------------
.. csv-table::
   :header: "Workstation", "Processors","Cores","Memory", "Local Disk"
   :widths: 12, 38, 5,5,5

   mcic-galaxy-srvr,two 3.47GHz six-core Intel® Xeon processors X5690,12, 94 GB,2.6 TB
   mcic-mac-srvr,two 2.93GHz six-core Intel® Xeon processors X5670,12, 64 GB,4.0 TB

3.3 Software Overview
----------------------
Following bioinformatics software are availabe through MCBL.

3.3.1 Commercial Software
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :header: "Application", "Version","Description","Contact"
   :widths: 10, 12, 40,15

   CLCBio Workbench,8.5.1,A comprehensive and user-friendly analysis package for analyzing comparing and visualizing next generation sequencing data,`Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_
   Blast2GO Pro,Pro,A complete framework for functional annotation and analysis,`Saranga Wijeratne <mailto:wijeratne.3@osu.edu>`_

3.3.2 Open Source Software
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. csv-table::
   :header: "Application", "Version","Description","Module Name"
   :widths: 10, 12, 40,10

   Bowtie,1.1.0/2-2.2.3,An ultrafast and memory-efficient tool for aligning sequencing reads to long reference sequences,Bowtie-<version>
   cd-hit,4.6.1,A very widely used program for clustering and comparing protein or nucleotide sequences,cd-hit-v<version>
   Cutadapt,1.4.2/1.8.1,Removes adapter sequences from high-throughput sequencing data,Cutadapt/<version>
   



