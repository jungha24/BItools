
1. annotate dbSNP to annovar input text file
~~~bashscript
/Users/jeongha/software/annovar/annotate_variation.pl -downdb -buildver hg38 -webfrom annovar avsnp147 humandb
/Users/jeongha/software/annovar/annotate_variation.pl -filter -out 220630_ALL_sig_eQTL_ANNOVAR_out -build hg38 -dbtype avsnp147 220630_ALL_sig_eQTL_ANNOVAR.txt humandb/
~~~
