clean_ngs
=========

Yet another adapter removal program for next generation sequencing 

clean_ngs - NGS Data Cleaning
=============================


SYNOPSIS
--------
    clean_ngs [OPTIONS] -adf ADAPTER.txt -if1 IN.fq -of1 OUT.fq
    clean_ngs [OPTIONS] -adf ADAPTER.txt -if1 IN_1.fq -if2 IN_2.fq -of1
    OUT_1.fq -of2 OUT_2.fq

DESCRIPTION
-----------
    Use adapters definition file ADAPTER.txt and remove the adapters from the
    input readfiles. The program writes out the cleansed reads and the
    rejected reads.

```
-h, --help
          Displays this help message.
    --version
          Display version information
    -v, --verbose
          Verbose mode.
    -vv, --very-verbose
          Very verbose mode.

  Input / Output Parameters:
    -adf, --adapter-file FILE
          Adapter definition file. See section Adapters File Format below for
          moreinformation. Valid filetypes are: txt and dat.
    -if1, --input-file1 FILE
          Input file 1. Valid filetypes are: fastq, fq, fastq.gz, fq.gz, txt,
          txt.gz, and dat.
    -if2, --input-file2 FILE
          Input file 2. Valid filetypes are: fastq, fq, fastq.gz, fq.gz, txt,
          txt.gz, and dat.
    -of1, --output-file1 FILE
          Output file 1. Valid filetypes are: fastq, fq, fastq.gz, fq.gz, txt,
          txt.gz, and dat.
    -of2, --output-file2 FILE
          Output file 2. Valid filetypes are: fastq, fq, fastq.gz, fq.gz, txt,
          txt.gz, and dat.
    -rf1, --rejected-file1 FILE
          Rejected file 1. Valid filetypes are: fastq, fq, fastq.gz, fq.gz,
          txt, txt.gz, and dat.
    -rf2, --rejected-file2 FILE
          Rejected file 2. Valid filetypes are: fastq, fq, fastq.gz, fq.gz,
          txt, txt.gz, and dat.

  Optional Parameters:
    -l, --min-len NUM
          Minimal length of sequencing.Set to 0 to turn offminimal length
          filter. In range [0..inf]. Default: 0.
    -L, --max-len NUM
          Maximal length of sequencing.Set to 0 to turn offmaximal length
          filter. In range [0..inf]. Default: 0.
    -q3, --qual-thresh3 NUM
          Quality threshold for 3-prime trimming.Set to 0 to turn off 3-prime
          trimming. In range [0..inf]. Default: 0.
    -q5, --qual-thresh5 NUM
          Quality threshold for 5-prime trimming.Set to 0 to turn off 5-prime
          trimming. In range [0..inf]. Default: 0.
```

ADAPTER DEFINITION FILE FORMAT
------------------------------
The adapter sequences are defined in an adapter definition file with the
extension ".txt" (dat is only allowed for Galaxy)

comment lines start with "#".

Each non-comment(non-empty) line is tab delimited

and has 7 fields (columns):

1. name of the sequence

2. sequence (N's are allowed and match any nucleotide, useful for
multiplexing)

3. fraction of identity between adapter sequence and target sequence
(threshold)

4. quality threshold

5. minimum length of overlap between adapter and target sequence

6. if set to >0 perform comparison with truncated adapter sequences (very
time consuming)

7. if set to 1 this is a leader sequence

VERSION
-------
clean_ngs version: 0.7
Last update March 2013

Installation
------------


Basic steps:

- [ ] Follow the instructions on seqan.de to install the seqan package (https://github.com/seqan/seqan)
- [ ] Follow the instructions on creating a sandbox
- [ ] Clone samBamStats.git to apps directory
- [ ] Update cmake configuration
- [ ] Make


This worked for me on a linux system:

```Shell
# clone seqan library
git clone https://github.com/seqan/seqan.git
# create a build directory
mkdir seqan-trunk-build
mkdir seqan-trunk-build/debug
cd seqan-trunk-build/debug
# configure a DEBUG build
cmake ../../seqan -DCMAKE_BUILD_TYPE=Debug
cd ../../seqan
# create a sandbox environment
./util/bin/skel.py repository sandbox/my_sandbox
# get sambamstat tool
cd sandbox/my_sandbox/apps/
git clone https://github.com/baj12/clean_ngs.git
cd ../../../../seqan-trunk-build/debug/
# let cmake learn about the changes
cmake .
# compile sambamstat
make clean_ngs
# basic test
bin/clean_ngs -h
```

Authors
-------
The initial upload was created by 
Manuel Holtgrewe <manuel.holtgrewe@fu-berlin.de>
and
Bernd Jagla <bernd.jagla@pasteur.fr>
