---
title: "Hands On"
layout: archive
permalink: /handsOn_prepare/
---  

The first step in running PIMBA is to prepare your data. PIMBA can be used with paired-end or single-end reads (the latter being single-index or dual-index). The output will be a Fasta file that can be used in the next step. In this tutorial, we will use only paired-end reads, but you can check at the end how to prepare single-end reads with dual and single-indexes.

**Paired-end reads**

Please place all your forward and reverse reads in one directory and ensure that forward reads contain "R1" and reverse reads contain "R2" in the file name.

```console  
./pimba_prepare.sh illumina <rawdata_dir> <output_reads> <num_threads> <adapters.txt> <min_length> <min_phred>
```

`rawdata_dir` = path with all the R1 and R2 reads file;\
`output_reads` = name for the output file;\
`num_threads` = number of threads;\
`adapters.txt` = tab separated 2-column file with all adapters and primers used for sequencing;\
`min_lenght` = The minimum length of the read after quality treatment;\
`min_phred` = Minimum PHRED score of a read after quality treatment.

Example:

```console  
  ./pimba_prepare.sh ilumina rawdata/ AllSamples 24 adapters.txt 100 20
```

**single-end reads with dual-index:**

In case your single-end reads have been multiplexed with dual-index, use the following command:

```console  
./pimba_prepare.sh iontorrent-dualindex  <rawdata.fastq> <barcodes.txt> <barcodes_reverse.txt> <barcodes.fasta> <barcodes_for_dir> <Primer_forward> <Primer_reverse> <num_threads> <output_name> <min_length> <min_phred>
```

`rawdata.fastq` = single file with all the reads to demultiplex;\
`barcodes.txt` = barcodes used as index in the 3' of the fragment;\
`barcodes_reverse.txt` = reverse complement of `barcodes.txt`;\
`barcodes.fasta` = fasta file for the `barcodes.txt`;\
`barcodes_for_dir` = path to all the barcodes.fasta and barcodes.txt used in the 5'  of the fragment. Each 3' barcode must have a fasta and txt file with all the associated 5' barcodes;\
`Primer_forward` = sequence of the forward primer;\
`Primer_reverse` = sequence of the reverse primer;\
`num_threads` = number of threads;\
`output_name` = name for the output fastq file;\
`min_length` = The minimum length of the read after quality treatment;\
`min_phred` = Minimum PHRED score of a read after quality treatment.

Example:

```console  
./pimba_prepare.sh iontorrent-dualindex rawdata_chip-3-4.fastq barcodes.txt barcodes_reverse.txt barcodes.fasta barcode_for/ TCCACTAATCACAAAGANATNGGNAC AGAAAATCATAATNAANGCNTGNGC 24 AllSamplesCOI.fastq 100 20
```

**single-end reads with single-index:**

In case your single-end reads have been multiplexed with single-index, use the following command:

```console  
./pimba_prepare.sh iontorrent-singleindex <rawdata.fastq> <prefix> <barcodes.txt> <barcodes.fasta> <primer> <num_threads> <output_name> <min_length> <min_phred>
```

`rawdata.fastq` = single file with all the reads to demultiplex;\
`prefix` = name that will precede the barcodes names;\
`barcodes.txt` = barcodes used as index in the 5' of the fragment;\
`barcodes.fasta` = fasta file for the `barcodes.txt`;\
`primer` = primer sequence;\
`num_threads` = number of threads;\
`output_name` = name for the output fastq file;\
`min_lenght` = The minimum length of the read after quality treatment;\
`min_phred` = Minimum PHRED score of a read after quality treatment.

Example:

```console  
./pimba_prepare.sh iontorrent-singleindex SN1-45.fastq SN1-45-ITS barcodes.txt barcodes.fasta ATGCGATACTTGGTGTGAAT 24 AllSamples
```