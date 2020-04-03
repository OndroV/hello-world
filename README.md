# hello-world
tutorial repository

#Description of my taxonomy assignment workflow. If you feel like getting some inspiration, great! Otherwise, no need to waste time with this incomplete description :D
I just had inspiration to write and share this bit now. When I have time, I'll review the scripts, write a full description and share :)

My merging script used your Bold-wh + gbif + ncbi's annotated HitTable. Blasting happens on the database websites. Only the Ncbi annotation is computed locally by https://github.com/Gurdhhu/bioinf_scripts/blob/master/annotate_blast_hits.py
For hits with >85% similarity, the output is more-or-less the same as from VascoElbrecht's Bold_web_hack (using All records Bold database). But <85% hits might be biased towards Animalia in Bold. Bold doesn't output score of alignment, so I couldn't compare them with Ncbi hits. I found that score is more accurate for poor alignments (they can get 100% similarity, but are just a few bp long).
Ncbi annotation takes time (~1h per 1000 OTUs) and creates several temporary files, up to 1GB each :D So we want to minimize the input files: before downloading HitTable from ncbi, I set the webpage to display only top 10 hits (1 would be enough, but 10 is minimum). Then I have a script to take only top-1-Hit per OTU. 
Also, the annotation gets stuck with some ncbi hits. It's rare, but when it happens, the script aborts with no results, after a few more hours. So, with another script I split the top-1-HitTable (like we split fasta file by 100 OTUs before Bold identification). Splitting helps track down the problematic hit. Then we can manually just remove it or replace by a lower hit from the same OTU and run again. 
Later, I'd like to find out what's wrong with those problematic hits. Until now they all had non-standard length of ncbi accession number. Standard is 10 characters. But most non-10-char hits work, it's just a few that are wrong.
