## Select a subset of sample for analysis based on metadata
Total: 8 groups with 40 samples in total (5 samples per each group)
[Metadata](https://www.ncbi.nlm.nih.gov/Traces/study/?WebEnv=NCID_1_109652569_130.14.18.97_5555_1556579220_2883070983_0MetA0_S_HStore&query_key=1)


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
```
for i in SRR8489620 SRR8489619 SRR8489618 SRR8489617 SRR8489614 SRR8489627 SRR8489626 SRR8489628 SRR8489629 SRR8489630; do echo $i > $i\_paired.txt; done

for i in SRR8489621 SRR8489622 SRR8489623 SRR8489624 SRR8489625 SRR8489603 SRR8489604 SRR8489605 SRR8489606 SRR8489608 SRR8489648 SRR8489649 SRR8489650 SRR8489651 SRR8489652 SRR8489632 SRR8489633 SRR8489634 SRR8489635 SRR8489636 SRR8489640 SRR8489641 SRR8489642 SRR8489643 SRR8489644 SRR8489594 SRR8489595 SRR8489596 SRR8489597 SRR8489598; do echo $i > $i\_single.txt; done
```

download and installing SRA toolkit

```
conda install -c bioconda sra-tools
sra-tools-2.9.1_1 
```
With release 2.9.1 of `sra-tools` we have finally made available the tool `fasterq-dump`, a replacement for the much older `fastq-dump` tool. As its name implies, it runs faster, and is better suited for large-scale conversion of SRA objects into FASTQ files that are common on sites with enough disk space for temporary files.

You can get more information about `fasterq-dump` in our Wiki at [https://github.com/ncbi/sra-tools/wiki/HowTo:-fasterq-dump](https://github.com/ncbi/sra-tools/wiki/HowTo:-fasterq-dump).

Storage policy - to avoid jam up the hard disk
```
/RAID_STORAGE2/stan/
```
- use --gzip flag

use script to download SRA reads (40 at the same time)</br>
```
nano dlSRAscript.sh 
chmod a+x dlSRAscript.sh
./dlSRAscript.sh 
```

If the below situation occur, go to the respective folder and rm lock files
```
2019-04-30T00:44:22 prefetch.2.9.1: 1) Downloading 'SRR8489641'...
2019-04-30T00:44:22 prefetch.2.9.1 warn: lock exists while copying file - Lock file /home/stan/ncbi/public/sra/SRR8489641.sra.lock exists: download canceled
```

### Quality check
```
for PE
1st run:
fastp -i rna1.F.fq.gz -I rna1.R.fq.gz -o out.rna1.F.fq.gz -O out.rna1.R.fq.gz -q 20 -P 100 -y 50 --detect_adapter_for_pe

2nd run:
fastp -i ${i} -I $(echo ${i}|sed s/_1/_2/) -o ${i}.out -O $(echo ${i}|sed s/_1/_2/).out -h ${i}.html -j ${i}.json -f 10 -q 20 -P 100 -y 50 --detect_adapter_for_pe

3rd run (TAKE THIS):
fastp -i ${i} -I $(echo ${i}|sed s/_1/_2/) -o ${i}.out -O $(echo ${i}|sed s/_1/_2/).out -h ${i}.html -j ${i}.json -f 15 -q 20 -P 100 -y 50 --detect_adapter_for_pe

create loop to run through PE fq.gz
nano fastp_PE.sh
chmod a+x fastp_PE.sh

for SE
nano fastp_SE.sh
chmod a+x fastp_SE.sh
1st run:
fastp -i ${i} -o ${i}.out -h ${i}.html -j ${i}.json -q 20 -P 100 -y 50

2nd run:
fastp -i ${i} -o ${i}.out -h ${i}.html -j ${i}.json -f 10 -q 20 -P 100 -y 50

3rd run(TAKE THIS):
fastp -i ${i} -o ${i}.out -h ${i}.html -j ${i}.json -f 15 -q 20 -P 100 -y 50

firefox CASE_J03.html
```

symlink
```
ln -s /RAID_STORAGE2/stan/FinalProject/PE/*.gz PE_fastq/
ln -s /RAID_STORAGE2/stan/FinalProject/SE/*.gz SE_fastq/
```

### Download human genome hg19
[hg19](http://hgdownload.cse.ucsc.edu/goldenpath/hg19/chromosomes/) - multiple files have to be concatenated into a single huge file
```
wget --timestamping 'ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/chromosomes/*'
cat *fa.gz > genome.fa.gz
zcat genome.fa.gz | grep -c ">"
93
zcat genome.fa.gz | grep ">"
gunzip genome.fa.gz
less genome.fa
ln -s /RAID_STORAGE2/stan/FinalProject/genome.fa ./
```

### Read alignment to human genome
```
conda install -c bioconda hisat2
```
