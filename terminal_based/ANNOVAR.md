
1. annotate dbSNP to annovar input text file
~~~bashscript
/Users/jeongha/software/annovar/annotate_variation.pl -downdb -buildver hg38 -webfrom annovar avsnp147 humandb
/Users/jeongha/software/annovar/annotate_variation.pl -filter -out 220630_ALL_sig_eQTL_ANNOVAR_out -build hg38 -dbtype avsnp147 220630_ALL_sig_eQTL_ANNOVAR.txt humandb/
~~~




2. annotate gene name
~~~bashscript
perl annotate_variation.pl -downdb -buildver hg38 -webfrom annovar refGene humandb
perl annotate_variation.pl -out /Users/jeongha/Dropbox/JH/2022/COVID/20220815_article_fig/functional_anno/COVID19_HGI_B1_ALL_20220403.10k.sig.output.txt -build hg38 /Users/jeongha/Dropbox/JH/2022/COVID/20220815_article_fig/functional_anno/COVID19_HGI_B1_ALL_20220403.10k.sig.input.txt humandb/
~~~
