### Lobstr-code
lobSTR: a short tandem repeat profiler for next generation sequencing data

#### downdload
1. source code: *lobSTR-4.0.6.tar.gz*
> http://lobstr.teamerlich.org/download.html
2. lobSTR v3.+ index *lobSTR_v3.0.2_hg19_resource_bundle.tar.gz*

#### install
~~~bashscript
tar -xzf lobSTR-4.0.6.tar.gz
cd lobSTR-4.0.6.tar.gz
./configure
make
make check # optional
sudo make install
~~~

#### usage
~~~bashscript
lobSTR \
  --p1 KRP5_1.fastq \
  --p2 KRP5_2.fastq \
  -q \
  --index-prefix ./lobstr_index/hg19_v3.0.2/lobstr_v3.0.2_hg19_ref/lobSTR_ \
  -o KRP5_lobstr \
  --rg-sample KRP5 --rg-lib KRP5
  
samtools sort -o KRP5_lobstr.aligned.sorted.bam KRP5_lobstr.aligned.bam 
samtools index KRP5_lobstr.aligned.sorted.bam

allelotype \
  --command classify \
  --bam KRP5_lobstr.aligned.sorted.bam \
  --noise_model ./lobSTR-4.0.6/models/illumina_v3.pcrfree \
  --out KRP5_lobstr_allelotype \
  --strinfo ./lobstr_index/hg19_v3.0.2/lobstr_v3.0.2_hg19_strinfo.tab \
  --index-prefix ./lobstr_index/hg19_v3.0.2/lobstr_v3.0.2_hg19_ref/lobSTR_
~~~

for more information visit http://lobstr.teamerlich.org/index.html

#### additional job
annotate gene information with snpEff
~~~bashscript
java -Xmx8g -jar /ssd-data/workspace/support/tool/snpEff_180608_v4.3t/snpEff/snpEff.jar GRCh37.75 -canon KRP5_lobstr_allelotype.vcf > KRP5_lobstr_allelotype.snpeff.vcf
~~~
