---
title: Tips for routine tools
categories:
  - bioinformatics
tags:
  - bioinformatics
---

1.hmmer

> convalign.py stockholm file.aln(file.fasta)
> 
> hmmbuild &#8211;amino file.hmm file.sth
> 
> hmmsearch -o file.hmm.hit &#8211;noali &#8211;nobias file.hmm targetPep.fasta
> 
> &nbsp;
> 
> &nbsp;

2.blast

短序列  
psiblast -query AT4G13850.1 -db ../../../conservation/subject/AT4G13850.1 -out AT4G13850.1.out -num\_iterations 3 -evalue 20000 -matrix PAM30 -comp\_based_stats 0

psiblast -query $(basename $@) -db /data7T/mercu-b-backup/pu b-data/NCBI-NR/nr -out $@ -outfmt 0 -num\_threads 8 -threshold 0.005 -eval ue 10 -max\_target\_seqs 1000 -num\_iterations 10 -inclusion_ethresh 0.002

#file.fasta由clustralw等多序列比对软件生成

psiblast -in\_msa file.fasta ../../../conservation/subject/AT4G13850.1 -out AT4G13850.1.out -num\_iterations 3 -evalue 20000 -matrix PAM30 -comp\_based\_stats 0

&nbsp;

#返回fasta格式的数据

blastdbcmd -entry NP_172083.1 -db /data7T/mercu-b-backup/pub-data/NCBI-NR/nr

#自定义输出格式

blastp -query 1PP2.L.fasta -db /data7T/mercu-b-backup/pub-data/NCBI-NR/nr -out 1PP2.L.fasta.out.0 -num_threads=8 **-outfmt='6 qseqid sseqid pident length slen evalue'**

http://www.ncbi.nlm.nih.gov/blast/html/sub_matrix.html

短序列
psiblast -query AT4G13850.1 -db ../../../conservation/subject/AT4G13850.1 -out AT4G13850.1.out -num_iterations 3 -evalue 20000 -matrix PAM30 -comp_based_stats 0

psiblast -query $(basename $@) -db /data7T/mercu-b-backup/pu b-data/NCBI-NR/nr -out $@ -outfmt 0 -num_threads 8 -threshold 0.005 -eval ue 10 -max_target_seqs 1000 -num_iterations 10 -inclusion_ethresh 0.002

#file.fasta由clustralw等多序列比对软件生成

psiblast -in_msa file.fasta ../../../conservation/subject/AT4G13850.1 -out AT4G13850.1.out -num_iterations 3 -evalue 20000 -matrix PAM30 -comp_based_stats 0

 

#返回fasta格式的数据

blastdbcmd -entry NP_172083.1 -db /data7T/mercu-b-backup/pub-data/NCBI-NR/nr

#自定义输出格式

blastp -query 1PP2.L.fasta -db /data7T/mercu-b-backup/pub-data/NCBI-NR/nr -out 1PP2.L.fasta.out.0 -num_threads=8 -outfmt=’6 qseqid sseqid pident length slen evalue’

http://www.ncbi.nlm.nih.gov/blast/html/sub_matrix.html


3.meme  [http://meme.sdsc.edu/meme/doc/meme.html]

> meme F1\_MEF.macs\_peaks.pv2000.bed.fa -dna -nmotifs 1000 -evt 0.001 -revcomp \  
> -mod anr -minsites 50 -maxsites 10000 \  
> -maxsize \`cat F1\_MEF.macs\_peaks.pv2000.bed.fa | wc -c\` \  
> -oc F1\_MEF.macs\_peaks.pv2000.meme
> 
> &nbsp;
> 
> &nbsp;

4.meme修改

> mcast调用mhhmscan出现错误 sh: line 1: 11764 Aborted
> 
> FATAL: mhmmscan failed with exit status 134, command run was: <code>
> 
> &nbsp;
> 
> Revise：
> 
> run <code> with another parameter &#8211;blocksize <maxsequencelength>

> &nbsp;
> 
> $(cell).macs\_peaks.pv2000.homer: $(cell).macs\_peaks.pv2000.bed
> 
> findMotifsGenome.pl $< mm9 $@ -size given -p 6  
> pythonmail2.py $@ $@
> 
> $(cell).macs\_peaks.pv2000.meme-fimo-uniprobe: $(cell).macs\_peaks.pv2000.bed.fa  
> fimo &#8211;output-qthresh 0.1 &#8211;max-seq-length 2.5e8 \  
> &#8211;oc $@ &#8211;max-stored-scores 1000000000 \  
> ~/soft/meme/db/motif\_databases/uniprobe\_mouse.meme $<  
> pythonmail2.py $@ $@  
> tail -n +2 $@/fimo.txt | cut -f 1 | sort | uniq -c | sed &#8216;s/^ *//' \  
> | awk &#8216;BEGIN{OFS=&#8221;\t&#8221;;FS=&#8221; &#8220;;}{print $$2,$$1}' | sort -k1,1 \  
> >$@/fimo.txt.motif.pattern.cnt  
> join -a1 -t &#8216; &#8216; -o 2.2,1.2 \  
> $@/fimo.txt.motif.pattern.cnt $(uniprobe_tf) \  
> >$@/fimo.txt.motif.tf.cnt  
> $(cell).macs\_peaks.pv2000.meme-mcast-uniprobe: $(cell).macs\_peaks.pv2000.bed.fa  
> mkdir -p $@  
> mhmm &#8211;type star &#8211;keep-unused &#8211;verbosity 2 \  
> /home/chentong/soft/meme/db/motif\_databases/uniprobe\_mouse.meme \  
> >$@/uniprobe_mouse.meme.mhmm  
> mhmmscan &#8211;fancy &#8211;allow-weak-motifs &#8211;p-thresh 0.0005 \  
> &#8211;max-gap 50 &#8211;e-thresh 10 &#8211;eg-cost 1 \  
> &#8211;blocksize \  
> \`gawk &#8216;{if(x<length()) x = length()}END{print x}' $<\` \  
> &#8211;verbosity 5 &#8211;pseudo-weight 4.0 \  
> $@/uniprobe_mouse.meme.mhmm $< \  
> >$@/mcast.txt  
> mhmm2html $@/mcast.txt >$@/mcast.html  
> pythonmail2.py $@ $@

&nbsp;

5.

6.

7.

8.

9.

10.

11.

12.

13.

14.

15.

16.

17.

18.

19.

20.
