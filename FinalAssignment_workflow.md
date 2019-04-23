## Select a subset of sample for analysis based on metadata
Total: 8 groups with 40 samples in total (5 samples per each group)
[Metadata](https://www.ncbi.nlm.nih.gov/Traces/study/?WebEnv=NCID_1_88064275_130.14.18.97_5555_1556025930_2637657709_0MetA0_S_HStore&query_key=14)


## Step 1: Find the data on NCBI
> [SRA sites](https://www.ncbi.nlm.nih.gov/sra?linkname=bioproject_sra_all&from_uid=517165)
> Input to obtain file: Accessions in a .txt 

```
conda create -n finalproject
conda activate finalproject
mkdir FinalProject
cd FinalProject/
```

create SraAccList.txt
PE
SE

for i in SRR8489619 SRR8489618 SRR8489617 SRR8489614 SRR8489627 SRR8489626 SRR8489628 SRR8489629 SRR8489630; do echo $i > $i\_paired.txt; done

download and installing SRA toolkit

```
conda install -c bioconda sra-tools
sra-tools-2.9.1_1 
```
With release 2.9.1 of `sra-tools` we have finally made available the tool `fasterq-dump`, a replacement for the much older `fastq-dump` tool. As its name implies, it runs faster, and is better suited for large-scale conversion of SRA objects into FASTQ files that are common on sites with enough disk space for temporary files.

You can get more information about `fasterq-dump` in our Wiki at [https://github.com/ncbi/sra-tools/wiki/HowTo:-fasterq-dump](https://github.com/ncbi/sra-tools/wiki/HowTo:-fasterq-dump).


use script to download SRA reads (40 at the same time)
nano dlSRAscript.sh 
chmod a+x dlSRAscript.sh
./dlSRAscript.sh 



