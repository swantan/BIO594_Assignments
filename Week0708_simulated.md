```
conda activate Week9.Ex
cd home/stan/Week9/Week9.Ex/simulated/fasqfiles
dDocent
wc -l Final.recode.vcf
```
```
3042 Final.recode.vcf
```

```
cd ..
head TotalRawSNPs.vcf
vcftools --vcf TotalRawSNPs.vcf  --max-missing 0.5 --maf 0.001 --minQ 20 --recode --recode-INFO-all --out TRS
```
output: TRS.log  TRS.recode.vcf
```
VCFtools - 0.1.15
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf TotalRawSNPs.vcf
	--recode-INFO-all
	--maf 0.001
	--minQ 20
	--max-missing 0.5
	--out TRS
	--recode

After filtering, kept 80 out of 80 Individuals
Outputting VCF file...
After filtering, kept 2993 out of a possible 3025 Sites
Run Time = 2.00 seconds
```

```
vcftools --vcf TRS.recode.vcf --minDP 5 --recode --recode-INFO-all --out TRSdp5
```

VCFtools - 0.1.15
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf TRS.recode.vcf
	--recode-INFO-all
	--minDP 5
	--out TRSdp5
	--recode

After filtering, kept 80 out of 80 Individuals
Outputting VCF file...
After filtering, kept 2993 out of a possible 2993 Sites
Run Time = 1.00 seconds

```

```
