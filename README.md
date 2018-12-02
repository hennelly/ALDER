# ALDER for inferring admixture

**ALDER** computes the weighted linkage disequilibrium (LD) statistic for making inference about popualtion admixture. 

Here's the link to the download: http://cb.csail.mit.edu/cb/alder/

### **Required input format**
- **Genotype data file**: ALDER requires genotype data to be provided in EIGENSTRAT format (.geno, .snp, and .ind files). Format conversion from several other common formats can be performed using the **CONVERTF** program provided with the EIGENSOFT package.

- **Parameter file**: The simplest invocation of ALDER uses the following parameters:

  - genotypename: /path/to/data.geno
  - snpname:      /path/to/data.snp
  - indivname:    /path/to/data.ind
  - admixpop:     testpopC
  - refpops:      refpopA;refpopB


### **1.) Convert .ped and .map files to Eigenstrat format using convertf** 


The ALDER package includes a directory labeled **CONVERTF**. We will use the scripts in this directory to convert files. 

For our purpose here, we will use  ".PED.EIGENSTRAT" to convert .map and .ped to **eigenstrat.geno**, **output.ind**, and **output.snp files**. 

```
touch par.PED.EIGENSTRAT.chr1
```

The basic format for the parameter file is: 
```
genotypename:    chr1.ped
snpname:         chr1.map
indivname:       chr1.ped
outputformat:    EIGENSTRAT
genotypeoutname: chr1.eigenstratgeno
snpoutname:      chr1.snp
indivoutname:    chr1.ind
familynames:     YES
```
We will run the convert command below: 

```
./convertf -p par.PED.EIGENSTRAT.chr1
```

## **2.) Prepare ALDER input files**

Create the parfile for ALDER
```
touch parfile.txt
```

**Preparing the parfile for ALDER**
```
genotypename: /directory/chr1.eigenstratgeno
snpname: /directory/chr1.snp
indivname: /directory/chr1.ind
admixpop: popAdmix
refpops: refA;refB
raw_outname: weightedLDdata
jackknife: YES
print_jackknife_fits: YES
chrom: 1
checkmap: YES
binsize: 0.0005
```
**Note: the .ind file needs the population names 


## **3.) RUN ALDER**

```
./alder -p parfile.txt
```



