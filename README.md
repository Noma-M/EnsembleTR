# EnsembleTR

EnsembleTR is a tool for ensemble Tandem Repeat (TR) calling. It takes one or more VCF files with TR genotypes for a panel of samples and outputs a consensus set of genotypes.


## Installation

```
python3 setup.py install --user
```

Type `EnsembleTR`. You should see the help message appear.

## Usage

To run EnsembleTR, use the following command

```
EnsembleTR --out output.vcf
           --ref ref.fa
           --vcfs vcf1.vcf,vcf2.vcf,...
```
Required parameters:
* **`--vcfs <file.vcf,[file2.vcf]>`** Comma separated list of input VCF files
* **`--ref`** Refererence genome (.fa)
* **`--out`** Path to output VCF file

## File formats

### VCF (`--vcfs`)
Both zipped and unzipped VCF files are accepted as input. EnsembleTR can currently process VCF files generated by [hipSTR](https://github.com/tfwillems/HipSTR), [GangSTR](https://github.com/gymreklab/GangSTR), [adVNTR](https://advntr.readthedocs.io/en/latest/#), and [ExpansionHunter](https://github.com/Illumina/ExpansionHunter).

### FASTA Reference genome (`--ref`)
You must input a reference genome in FASTA format. This must be the same reference build used for TR calling in input files.

### VCF (`--out`)
For more information on VCF file format, see the [VCF spec](http://samtools.github.io/hts-specs/VCFv4.2.pdf). EnsembleTR output VCF file contains several fields that are described below.

#### INFO fields

INFO fields contain aggregated statistics about each TR. The following custom fields are added:

| **FIELD** | **DESCRIPTION** |
|-----------|------------------|
| START | Start position of the TR |
| END | End position of the TR |
| PERIOD | Length of the repeat unit |
| RU | Repeat motif | 
| METHODS| Methods that attempted to genotype this locus (AdVNTR, EH, HipSTR, GangSTR)| 

#### FORMAT fields
FORMAT fields contain information specific to each genotype call. The following custom fields are added:

| **FIELD** | **DESCRIPTION** |
|-----------|------------------|
| GT | Genotype |
| GB | Base pair difference from ref allele |
| NCOPY | Genotype given in number of copies of the repeat motif |
| EXP | Boolean showing if the genotype alleles were expanded |
| SCORE | Score of the consensus call |
| GTS | Method(s) that support the consensus call |
| ALS | Number of times each bp difference was seen across all calls |
| INPUTS | Raw calls | 

Score is calculated by aggregating quality information from calls that are getting merged at each locus.

## Using statSTR on EnsembleTR files

You can use [statSTR](https://trtools.readthedocs.io/en/latest/source/statSTR.html) from [TRTools](https://trtools.readthedocs.io/en/latest/index.html) to compute various per-locus statistics for EnsembleTR .VCF files.

For example, to compute per-locus allele frequency use the following command:

```
statSTR --vcf EnsembleTR_file.vcf.gz
        --vcftype hipstr
        --afreq
        --out EnsembleTR_per_locus_allele_frequency
```

## Version I of EnsembleTR calls on samples from 1000 Genomes Project and H3Africa

Chromosome 1 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr1_filtered.vcf.gz) (575 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr1_filtered.vcf.gz.tbi)

Chromosome 2 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr2_filtered.vcf.gz) (568 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr2_filtered.vcf.gz.tbi)

Chromosome 3 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr3_filtered.vcf.gz) (472 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr3_filtered.vcf.gz.tbi)

Chromosome 4 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr4_filtered.vcf.gz) (427 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr4_filtered.vcf.gz.tbi)

Chromosome 5 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr5_filtered.vcf.gz) (414 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr5_filtered.vcf.gz.tbi)

Chromosome 6 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr6_filtered.vcf.gz) (413 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr6_filtered.vcf.gz.tbi)

Chromosome 7 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr7_filtered.vcf.gz) (374 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr7_filtered.vcf.gz.tbi)

Chromosome 8 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr8_filtered.vcf.gz) (342 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr8_filtered.vcf.gz.tbi)

Chromosome 9 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr9_filtered.vcf.gz) (324 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr9_filtered.vcf.gz.tbi)

Chromosome 10 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr10_filtered.vcf.gz) (330 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr10_filtered.vcf.gz.tbi)

Chromosome 11 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr11_filtered.vcf.gz) (357 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr11_filtered.vcf.gz.tbi)

Chromosome 12 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr12_filtered.vcf.gz) (408 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr12_filtered.vcf.gz.tbi)

Chromosome 13 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr13_filtered.vcf.gz) (258 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr13_filtered.vcf.gz.tbi)

Chromosome 14 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr14_filtered.vcf.gz) (261 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr14_filtered.vcf.gz.tbi)

Chromosome 15 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr15_filtered.vcf.gz) (238 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr15_filtered.vcf.gz.tbi)

Chromosome 16 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr16_filtered.vcf.gz) (259 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr16_filtered.vcf.gz.tbi)

Chromosome 17 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr17_filtered.vcf.gz) (285 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr17_filtered.vcf.gz.tbi)

Chromosome 18 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr18_filtered.vcf.gz) (206 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr18_filtered.vcf.gz.tbi)

Chromosome 19 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr19_filtered.vcf.gz) (256 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr19_filtered.vcf.gz.tbi)

Chromosome 20 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr20_filtered.vcf.gz) (187 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr20_filtered.vcf.gz.tbi)

Chromosome 21 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr21_filtered.vcf.gz) (96 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr21_filtered.vcf.gz.tbi)

Chromosome 22 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr22_filtered.vcf.gz) (119 MB) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/split/ensemble_chr22_filtered.vcf.gz.tbi)

## Version I of reference SNP+TR haplotype panel for imputation of TR variants

### Dataset description

Phased variants of 3,202 samples from the 1000 Genomes Project (1kGP).

TRs imputed from 3,202 1kGP samples.

Total 27,185,239 variants + 1,089,670 TR markers

All the coordinates are based on the hg38 human reference genome.

### Availability

Chromosome 1 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr1_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr1_final_SNP_merged.vcf.gz.csi)

Chromosome 2 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr2_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr2_final_SNP_merged.vcf.gz.csi)

Chromosome 3 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr3_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr3_final_SNP_merged.vcf.gz.csi)

Chromosome 4 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr4_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr4_final_SNP_merged.vcf.gz.csi)

Chromosome 5 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr5_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr5_final_SNP_merged.vcf.gz.csi)

Chromosome 6 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr6_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr6_final_SNP_merged.vcf.gz.csi)

Chromosome 7 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr7_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr7_final_SNP_merged.vcf.gz.csi)

Chromosome 8 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr8_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr8_final_SNP_merged.vcf.gz.csi)

Chromosome 9 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr9_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr9_final_SNP_merged.vcf.gz.csi)

Chromosome 10 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr10_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr10_final_SNP_merged.vcf.gz.csi)

Chromosome 11 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr11_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr11_final_SNP_merged.vcf.gz.csi)

Chromosome 12 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr12_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr12_final_SNP_merged.vcf.gz.csi)

Chromosome 13 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr13_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr13_final_SNP_merged.vcf.gz.csi)

Chromosome 14 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr14_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr14_final_SNP_merged.vcf.gz.csi)

Chromosome 15 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr15_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr15_final_SNP_merged.vcf.gz.csi)

Chromosome 16 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr16_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr16_final_SNP_merged.vcf.gz.csi)

Chromosome 17 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr17_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr17_final_SNP_merged.vcf.gz.csi)

Chromosome 18 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr18_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr18_final_SNP_merged.vcf.gz.csi)

Chromosome 19 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr19_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr19_final_SNP_merged.vcf.gz.csi)

Chromosome 20 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr20_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr20_final_SNP_merged.vcf.gz.csi)

Chromosome 21 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr21_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr21_final_SNP_merged.vcf.gz.csi)

Chromosome 22 [VCF file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr22_final_SNP_merged.vcf.gz) and [tbi file](https://ensemble-tr.s3.us-east-2.amazonaws.com/phased-split/chr22_final_SNP_merged.vcf.gz.csi)

### Usage

Use [Beagle](https://faculty.washington.edu/browning/beagle/beagle.html) to impute TRs into SNP data:

```
java -Xmx4g -jar beagle.version.jar \
            gt=SNPs.vcf.gz \
            ref=${chrom}_final_SNP_merged.vcf.gz \
            out=imputed_TR_SNPs
```

