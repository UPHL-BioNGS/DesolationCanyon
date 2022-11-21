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

## Create file with relevant header

```bash

```

## Create mash sketch file


## Upload to Zenodo

current address is

## Download from Zenodo

wget <>
