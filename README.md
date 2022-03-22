## PMcalling

PMcalling extracts information such as mutation sites and their frequencies in the pooled samples from the mapping results of the sample sequence to the reference genome into the result files and excludes false positive results that may come from sequencing errors, contamination by other species, and interference from genomic repeat regions. PMcalling can be used not only for the analysis of microbial community sample sin specific environments, but also for genomic differential locus analysis of eukaryotic mixed samples such as tumor tissues.

## Workflow

### 1. Prepare input files

**1. Prepare input files**

Mapping the NGS reads of the pooled sample and the isogenic control to the reference genome, the result files are then sorted according to the position of the reference genome sequence to obtain pooled.sort.bam and isogenic.sort.bam, which are used as the input files for PMcalling.

### **2. PMcalling usage and parameter description** 

PMcalling can be installed and run on a computer with a Linux or macQS operating system and a Java runtime environment. PMcalling is simple to run with a single command: 

```
java -cp .:java-getopt-1.0.13.jar Src/PM_V1 -P pooled.sort.bam --Iso isogenic.sort.bam -R Reference.fna --MLength 0.95 --MQuality 40 --MinRead 3 --MinFreq 0.004 --End 0 --PMDep 150 --FixDep 150 --FixFreq 0.97 --MisMatch 3 --MisLen 30 --Out example.vcf
```

#### Required Arguments:

**-P**, BAM file of pooled sample.

**--Iso**, BAM file of isogenic control. 

**-R**, file of reference genome sequence. 

#### Optional Arguments:

**--MLength**, the minimum proportion of a single reads matching the reference genomic sequence, 0.95 is recommended. 

**--MQuality**, the minimum quality score for a single base matching the reference genomic sequence, 40 is recommended. 

**--MinRead**, the minimum number of reads supporting the mutation site, 3 is recommended. 

**--MinFreq**, the minimum proportion of the number of reads supporting the mutation site, 0.004 is recommended. 

**--End**, the minimum distance of the mutation site from the endpoint of the reads, 0 is recommended. 

**--PMDep**, the minimum number of reads covering the mutation site, 350 is recommended. 

**--FixDep**, the minimum number of reads covering the fixed mutation site, 350 is recommended. 

**--FixFreq**, the minimum frequency of fixed mutation site, 0.97 is recommended. 

**--MisMatch**, the maximum value of the mutation site allowed to exist between reads and reference genomic sequences within a certain range (determined by MisLen), 3 is recommended. 

**--MisLen**, the window length for counting the number of mutation sites between the reads and the reference genomic sequence, 30 is recommended. 

**--Out**, the output file name.

### **3. Output files**

**example.vcf.fixed.vcf**, VCF file of the fixed mutation sites found in the pooled sample.

**example.vcf.indel.vcf**, VCF file of the insertion–deletion mutations (indels) found in the pooled sample.

**example.vcf.PM.vcf**, VCF file of the polymorphic mutations (PMs) found in the pooled sample.

**example.vcf.PM.fasta**, the nucleotide sequences in the regions where PMs were found in the pooled sample.

 

**example.vcf_iso.fixed.vcf**, VCF file of the fixed mutation sites found in the isogenic control.

**example.vcf_iso.indel.vcf**, VCF file of the insertion–deletion mutations (indels) found in the isogenic control.

**example.vcf_iso.PM.vcf**, VCF file of the polymorphic mutations (PMs) found in the isogenic control.

**example.vcf_iso.PM.fasta**, the nucleotide sequences in the regions where PMs were found in the isogenic control.