# artic-measles
This pipeline complements [``RAMPART``](https://github.com/artic-network/rampart).

## Table of contents


  * [Requirements](#requirements)
  * [Installation](#installation)
  * [Setting up your run](#setting-up-your-run)
  * [Checklist](#checklist)
  * [Running RAMPART](#running-rampart)
  * [RAMPART command line options](#rampart-command-line-options)
  * [Reference FASTA](#reference-fasta)


## Requirements
This pipeline will run on MacOS and Linux. An install of Miniconda will make the setup of this pipeline on your local machine much more streamlined. To install Miniconda, visit here https://conda.io/docs/user-guide/install/ in a browser, select your type of machine (mac or linux) and follow the link to the download instructions. We recommend to install the 64-bit Python 3.6 version of Miniconda. 

## Installation
Clone this repository:

```
git clone https://github.com/artic-network/artic-measles.git
```

1. Create the conda environment.
This may take some time, but will only need to be done once. It allows the pipeline to access all the software it needs, including RAMPART.

```
cd artic-measles
conda env create -f environment.yml
```

2. Activate the conda environment.

```
conda activate artic-measles
```

## Setting up your run


If you have a ``run_configuration.json`` file and a ``barcodes.csv`` file, you can run RAMPART with very few command line options. A template of the configuration files needed to run both RAMPART and the downstream analysis pipeline is provided in the examples directory.

The run_configuration.json can specify the path to your basecalled reads or alternatively you can input that information on the command line. `basecalledPath` should be set to wherever MinKNOW/guppy is going to write its basecalled files. If you want alter where the annotations files from RAMPART or the analysis files from the downstream pipeline are put, you can add the optional ``"annotatedPath"`` and ``"outputPath"`` options. By default the annotations are written to a directory called ``annotations`` and the analysis output is written to a directory called ``analysis``.

```
run_configuration.json

{
  "title": "MinION_run_example",
  "basecalledPath": "fastq_pass",
  "referencesLabel":"display_name"
}
```

Optional for RAMPART, the ``barcodes.csv`` file describes which barcode corresponds to which sample. Note that you can have more than one barcode for each sample, but they will be merged in the analysis.

```
barcodes.csv

sample,barcode
sample1,BC01
sample2,BC02
sample3,BC03
sample4,BC04
```

## Checklist

- The conda environment ``artic-measles`` is active.
- ``barcodes.csv`` file with sample to barcode mapping either in the current directory or the path to it will need to be provided.
- ``annotations`` directory with csv files from RAMPART
- The path to basecalled ``.fastq`` files is provided either in the ``run_configuration.json`` or it will need to be specified on the command line.

## Running RAMPART

Create run folder:

```
mkdir [run_name]
cd [run_name]
```

Where `[run_name]` is whatever you are calling todays run (as specified in MinKNOW).


With this setup, to run RAMPART:

```
rampart --protocol path/to/artic-measles/rampart
```

Open a web browser to view [http://localhost:3000](http://localhost:3000)

More information about RAMPART can be found [here](https://github.com/artic-network/rampart).

## RAMPART command line options

```
usage: rampart [-h] [-v] [--verbose] [--ports PORTS PORTS]
               [--protocol PROTOCOL] [--title TITLE]
               [--basecalledPath BASECALLEDPATH]
               [--annotatedPath ANNOTATEDPATH]
               [--referencesPath REFERENCESPATH]
               [--referencesLabel REFERENCESLABEL]
               [--barcodeNames BARCODENAMES [BARCODENAMES ...]]
               [--annotationOptions ANNOTATIONOPTIONS [ANNOTATIONOPTIONS ...]]
               [--clearAnnotated] [--simulateRealTime SIMULATEREALTIME]
               [--devClient] [--mockFailures]
```
