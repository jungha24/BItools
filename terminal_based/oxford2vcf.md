### start from extension .impute2
### bunch of files from .sampleA.interval1.impute2 to .sampleZ.intervaln.impute2

1. 
~~~bashscripts
# download .impute2 files for COV-CCO-0011 sample
aws s3 cp s3://211216-covid-ap-northeast-2/1000g_output/ ./COV-CCO-0011/ --recursive --include "COV-CCO-0011.*"

# convert .impute2 to vcf
## 'ref-first' option is required to assign reference allele
## --hard-call-threshold 0.1
for f in *.impute2; do /data/support/tool/plink2-2 --gen ${f} 'ref-first' --sample ../../impute2_input/COV-CCO-0011_WGS.minac1.chr1.sample --oxford-single-chr ${${f#*.}%%.*} --recode vcf --out ${f}.plink2 --hard-call-threshold 0.1; done

# still some varaints display switched ref/alt allele 
## apply --ref-from-fa
for f in *.plink2.vcf; do /data/support/tool/plink2-2 --vcf ${f} --ref-from-fa force ../../GCA_000001405.15_GRCh38_no_alt_plus_hs38d1_analysis_set.fna --recode vcf --out ${f%.*}refcheck; done

for f in *.plink2refcheck.vcf; do bgzip -c ${f} > ${f}.gz; done
for f in *.plink2refcheck.vcf.gz; do tabix -p vcf ${f}; done

# concate vcfs 
bcftools concat *.plink2refcheck.vcf.gz -Oz -o COV-CCO-0011.phased.imute2.plink2refcheck.vcf.gz

# add 'chr' to all CHROM
bcftools annotate --rename-chrs chr_name_conv.txt COV-CCO-0011.phased.imute2.plink2refcheck.vcf.gz -Oz -o COV-CCO-0011.phased.impute2.plink2refcheck.reheader.vcf.gz

# sort vcf by genomic position
zcat COV-CCO-0011.phased.impute2.plink2refcheck.reheader.vcf.gz | awk '$1 ~ /^#/ {print $0; next} {print $0| "sort -k1,1V -k2n"}' > COV-CCO-0011.phased.impute2.plink2refcheck.reheader.sort.vcf

bgzip -c COV-CCO-0011.phased.impute2.plink2refcheck.reheader.sort.vcf > COV-CCO-0011.phased.impute2.plink2refcheck.reheader.sort.vcf.gz

# [optional] convert VCF v4.3 to v4.2 (vcftools does not support v4.3)
gunzip -c COV-CCO-0011.phased.impute2.plink2refcheck.reheader.sort.vcf.gz| sed 's/^##fileformat=VCFv4.3/##fileformat=VCFv4.2/' - | bgzip -c > COV-CCO-0011.phased.impute2.plink2refcheck.reheader2.sort.vcf.gz
~~~

