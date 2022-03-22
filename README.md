## PMcalling

PMcalling is a protocol for detecting low-frequency polymorphic mutations (PMs). PMcalling extracts information such as mutation sites and their frequencies in the pooled samples from the mapping results of the sample sequence to the reference genome into the result files and excludes false positive results that may come from sequencing errors, contamination by other species, and interference from genomic repeat regions. PMcalling can be used not only for the analysis of microbial community sample sin specific environments, but also for genomic differential locus analysis of eukaryotic mixed samples such as tumor tissues.

## Workflow

### 1. Prepare input files

Mapping the NGS reads of the pooled sample and the isogenic control to the reference genome, the result files are then sorted according to the position of the reference genome sequence to obtain pooled.sort.bam and isogenic.sort.bam, which are used as the input files for PMcalling.

### **2. PMcalling usage and parameter description** 

PMcalling can be installed and run on a computer with a Linux or macQS operating system and a Java runtime environment. PMcalling is simple to run with a single command (the recommended parameters are as follows): 

```
java -cp . -jar PMcalling.jar \0
-P pooled.sort.bam \
-R Reference.fa \
--MLength 0.95 \
--MQuality 40 \
--MinRead 3 \
--MinFreq 0.004 \
--end_distance 0 \
--PMDep 350 \
--FixDep 350 \
--FixFreq 0.97 \
--MisMatch 3 \
--MisLen 30
--out test.vcf
```

#### Required Arguments:

**-P/--pool**: sored bam file of pooled sample.

**-R/--ref**: file of reference genome sequence (fasta format).

#### Optional Arguments:

**-S/--strand**: Single-read (1) or paired-read(2)(int). defult:1

**-I/--iso**: The input of isofile. The isogenic control filter needed.

**-T/--tail**: Whether it need to be tail-test filter(0/1 No/Yes)(int). default:1

**-K/--flapping**: Whether it need to be Flapping indel filter(0/1 No/Yes)(int). default:1

**-Q/--MQuality**: The minimum mapping quality(int). deault: 35

**-L/--MLength**: The minimun mapping length rate(doubale value). default: 0.90

**-M/--MinRead**: The minimun read numbers of minor allele in SNP loci(int). default: 4

**-F/--MinFreq**: The minimun frequency of minor allele in SNP loci(double value). default: 0.005

**-C/--MisLen**: The minimum number of bases between two adjacent mismatching bases on a single read(int). default: 50

**-N/--MisMatch**: The maximum number of bases mismatched between the sample read and the reference genome(int). default: 3

**-E/--baseq**: The minimum base quality(int). default: 20

**-V/--pvalue**: The minimum p-value of T-test(double). default: 0.001

**-i/--indel_distance**: The minimum number of bases between right mismatch and indel loci(int). default: 6

**-e/--end_distance**: The minimum number of bases of mismatch from end of read(int). default: 6

**-W/--window**: The length of window(int). default: 20000

**-O/--overlap**: The overlap length between two windows(int). default: 1000

**-D/--PMDep**: The minimun read number of PM loci(int). default: 15

**-A/--FixDep**: The minimun read number of fixed mutation(int). default: 15

**-B/--FixFreq**: The minimum frequency of fixed mutation(double). default: 0.97

**-K/--flapping**: 1: filter the false-PM caused by indel loci in non-PM read

0: pass the flapping indel filter

**-d/--max_coverage**: The maximun depth of loci(int). default: 8000

**-m/--merge**: The minimun number of bases of indels located were merged(int). default: 0

**-H/--homo**: The minimum number of homopolymer bases of homopolymer indel filter(int). default:4

**-b/--bed**: One or more genomic intervals over which to operate in bed file.(String).

### **3. Output files**

**example.vcf.fixed.vcf**, VCF file of the fixed mutation sites found in the pooled sample.

**example.vcf.indel.vcf**, VCF file of the insertion–deletion mutations (indels) found in the pooled sample.

**example.vcf.PM.vcf**, VCF file of the polymorphic mutations (PMs) found in the pooled sample.

**example.vcf.PM.fasta**, the nucleotide sequences in the regions where PMs were found in the pooled sample.

 

**example.vcf_iso.fixed.vcf**, VCF file of the fixed mutation sites found in the isogenic control.

**example.vcf_iso.indel.vcf**, VCF file of the insertion–deletion mutations (indels) found in the isogenic control.

**example.vcf_iso.PM.vcf**, VCF file of the polymorphic mutations (PMs) found in the isogenic control.

**example.vcf_iso.PM.fasta**, the nucleotide sequences in the regions where PMs were found in the isogenic control.
