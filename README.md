# pybio: basic genomics toolset

pybio is a Python 3 framework for basic genomics operations. The package is a dependency to [apa](https://github.com/grexor/apa) (alternative polyadenylation) and [RNAmotifs2](https://github.com/grexor/rnamotifs2) (motif cluster analysis). The pybio package provides:

+ automatized download of genome assemblies from Ensembl and STAR indexing,
+ automatized download of genome annotations from Ensembl GTF with fast-searching capabilities,
+ Fasta, Fastq, bedGraph and other file format handling,
+ motif sequence searches,
+ alternative polyadenylation site-pair classification (same-exon, skipped-exon, composite-exon),
+ and other.

## Installation

A few steps of how to download and setup pybio.

### Close the GitHub repository

For now the most direct way of installing pybio is to clone the repository and add the containing folder to PYTHONPATH:

```
git clone https://github.com/grexor/pybio.git
```

If, for example, you installed pybio to /home/user, you would add this command to the .profile file in the same folder:

```
export PYTHONPATH=$PYTHONPATH:/home/user
```

### Dependencies

There are a few software tools pybio depends on:

* STAR aligner, `sudo apt-get install rna-star`
* pysam Python module, `sudo apt-get install python-pysam`

## Documentation

Here we provide basic pybio usage examples.

### Downloading and preparing Ensembl genomes

In the folder pybio/genomes, there are several .sh scripts you can use to automatically download and pre-process Ensembl genomes. Dependencies require you to have [STAR](https://github.com/alexdobin/STAR) installed. For example, to download and prepare the hg38 Ensembl v98, simply run:

```
cd pybio/genomes
./hg38.download.ensembl98.sh
```



## Authors

[pybio](https://github.com/grexor/pybio) is developed and supported by [Gregor Rot](https://grexor.github.io).

## Reporting problems

Use the [issues page](https://github.com/grexor/pybio/issues) to report issues and leave suggestions.
