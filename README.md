# DesolationCanyon
Basic instructions on how to create a mash *msh file for all prokaryotic representative genomes in NCBI genomes.

Dependencies
- mash
- datasets

## Get IDs for representative sequences

```bash
datasets summary genome taxon bacteria --reference --as-json-lines | \
  dataformat tsv genome --fields accession,assminfo-refseq-category,organism-name --elide-header | \
  grep representative | tee > representative_genomes.txt | cut -f 1 > genome_ids.txt
```

## Download representative sequences

```bash
datasets download genome accession --inputfile genome_ids.txt --filename rep-genomes.zip
```

## Decompress file
```bash
unzip rep-genomes.zip
```

These files are great and all, but this is what the header looks like:
```
$ head ncbi_dataset/data/GCF_902373765.1/GCF_902373765.1_MGYG-HGUT-01304_genomic.fna
>NZ_CABKNM010000001.1 [Clostridium] spiroforme isolate MGYG-HGUT-01304, whole genome shotgun sequence
CCATGTTGGTTGATTAATGTTCAGTAATCAGTTCTAGTACAGCAGTCAGTGTAAGCGGCGGCTGGACTCGTGCTTGTGTA
TTTCTTTACATACGACAAATAAGGCGTTGTAATCAATCGCAACTTGGGCTTGCCTTTTATGATTGACAAAAAAGGAAATT
```

Also, representative genomes DO contain their plasmid sequences
```
$ grep ">" ncbi_dataset/data/GCF_008632635.1/GCF_008632635.1_ASM863263v1_genomic.fna
>NZ_CP043953.1 Acinetobacter baumannii strain K09-14 chromosome, complete genome
>NZ_CP043954.1 Acinetobacter baumannii strain K09-14 plasmid pK09-14, complete sequence
```

Right now there's no incentive to remove plasmid sequences

## Create file with relevant header
Spaces and commas need to be removed. Brackets ([]) need to stay because they MEAN something.

```bash
cat  ncbi_dataset/data/*/*.fna  | sed 's/ /_/g' | sed 's/,//g' > rep-genomes.fasta
```

## Create mash sketch file
```bash
mash sketch rep-genomes.fasta
```

## Upload to Zenodo

The current size is
```bash
ls -h rep-genomes.msh
```

current address is

## Download from Zenodo

wget <>
