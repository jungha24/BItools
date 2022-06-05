
#### purpose: read mutant library of target gene with pacbio HiFi sequencing and check the condition of library

[1] align filtered fasta to reference with pacbio pbmm2
~~~bashscript
/ssd-data/workspace/support/tool/pacbio/smrtcmds/bin/pbmm2 align MECP2_REF.fasta MECP2.hifi_reads.length.fasta MECP2.hifi_reads.length.bam --log-level INFO
samtools sort -O bam -o MECP2.hifi_reads.length.sorted.bam MECP2.hifi_reads.length.bam
samtools index MECP2.hifi_reads.length.sorted.bam
~~~


