# pybio: basic genomics toolset

* [About](#about)
* [Installation](#installation)
* [Documentation](#documentation)
  * [Downloading Ensembl genomes](#downloading-Ensembl-genomes)
  * [Retrieving genomic sequence](#retrieving-genomic-sequence)
  * [Annotate genomic position](#annotate-genomic-position)
  * [Importing genome annotation](#importing-genome-annotation)
* [Authors](#authors)
* [Reporting problems](#reporting-problems)

## About

pybio is a Python 3 framework for basic genomics operations. The package is a dependency to [apa](https://github.com/grexor/apa) (alternative polyadenylation) and [RNAmotifs2](https://github.com/grexor/rnamotifs2) (motif cluster analysis). The pybio package provides:

+ automatized download of genome assemblies from Ensembl and STAR indexing,
+ automatized download of genome annotations from Ensembl GTF with fast-searching capabilities,
+ Fasta, Fastq, bedGraph and other file format handling,
+ motif sequence searches,
+ alternative polyadenylation site-pair classification (same-exon, skipped-exon, composite-exon),
+ and other.

## Installation

A few steps of how to download and setup `pybio`.

### Clone the GitHub repository

For now the most direct way of installing pybio is to clone the repository and add the containing folder to PYTHONPATH:

```
git clone https://github.com/grexor/pybio.git
```

If, for example, you installed `pybio` to `/home/user/pybio`, you would add this command to the .profile file in the same folder:

```
export PYTHONPATH=$PYTHONPATH:/home/user
export PATH=$PATH:/home/user/pybio/bin
```

### Dependencies

There are a few software tools pybio depends on:

* [STAR aligner](https://github.com/alexdobin/STAR), `sudo apt-get install rna-star`
* [pysam](https://pysam.readthedocs.io/en/latest/api.html), `sudo apt-get install python-pysam`
* [numpy](https://numpy.org/), `sudo apt-get install python-numpy`
* [Salmon](https://combine-lab.github.io/salmon/getting_started/), download and install from Salmon webpage
* [samtools](http://www.htslib.org), `sudo apt-get install samtools`

## Documentation

Here we provide basic `pybio` usage examples.

### Downloading Ensembl genomes

In the folder `pybio/genomes`, there are `.sh scripts` you can use to automatically download and pre-process Ensembl genomes. For example, to download and prepare the hg38 Ensembl v98, simply run:

```
cd pybio/genomes
./hg38.download.ensembl98.sh
```

This will download the FASTA sequence, GTF and TAB annotation (via Biomart) of the genome, and create several folders:

```
hg38.assembly.ensembl98           # FASTA files of the genome, each chromosome in a separate file
hg38.annotation.ensembl98         # Annotation in GTF and TAB format
hg38.assembly.ensembl98.star      # STAR index, GTF annotation aware
hg38.transcripts.ensembl98        # transcriptome, this is the Ensembl "cDNA" file in FASTA format
hg38.transcripts.ensembl98.salmon # Salmon index of the transcriptome
```

### Retrieving genomic sequence

To retrieve stretches of genomic sequence, we use the seq(genome, chr, strand, position, upstream, downstream) method:

```
pybio.genomes.seq("hg38", "1", "+", 450000, -20, 20) # returns 'TACCCTGATTCTGAAACGAAAAAGCTTTACAAAATCCAAGA' for hg38, Ensembl v98
```

The above command fetches the chr1 sequence from 450000-20..450000+20, the resulting sequence is of length 41.

### Annotate genomic position

Given a genomic position, we can retrieve the gene at the position and the closest upstream and downstream gene on the same strand:

```
(gene_up, gene_id, gene_down, gene_interval, gene_feature) = pybio.genomes.annotate("hg38", "1", "-", 450000)
```

The above command would return:

```
      gene_id: ENSG00000237094
gene_interval: (379972, 450701, 'i')
 gene_feature: 'intron'
      gene_up: 'ENSG00000284733'
    gene_down: 'ENSG00000228463'
```

There is gene ENSG00000237094 at position 450000, specifically the position is in an intron of the gene spanning the region 379972..450701.

### Importing genome annotation

pybio imports genome annotations from Ensembl or from a GTF file. The Ensembl import is from the TAB separated file generated by querying Biomart.

## Authors

[pybio](https://github.com/grexor/pybio) is developed and supported by [Gregor Rot](https://grexor.github.io).

## Reporting problems

Use the [issues page](https://github.com/grexor/pybio/issues) to report issues and leave suggestions.
