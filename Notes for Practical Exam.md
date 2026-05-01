1. From your home directory, make a new directory to hold fastq files called 'analysis' (2 points)

mkdir /home/users/lhi1001/gen711-811/analysis

2. Copy the fastq files /tmp/gen711_2023/Sample1.fastq and /tmp/gen711_2023/Sample2.fastq directly into the 'analysis' directory without changing your current directory. (2 points, partial credit if you need to change directories first)

cp /home/users/lhi1001/gen711-811/shell_data/untrimmed_fastq/*.fastq /home/users/lhi1001/gen711-811/analysis/

3. Use an absolute path to change your current working directory to the 'analysis' folder/directory. (2 points, partial credit for using a relative path)

cd /home/users/lhi1001/gen711-811/analysis

4. The fastq file you just copied is data from the UNH genome center. This is the first time you've ever seen these FASTQs. To confirm that the format of the FASTQs look ok, view one of the two files and paste the top 4 lines of the file below. (4 points)

head -4 SRR097977.fastq 

@SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
TATTCTGCCATAATGAAATTCGCCACTTGTTAGTGT
+SRR097977.1 209DTAAXX_Lenski2_1_7:8:3:710:178 length=36
CCCCCCCCCCCCCCC>CCCCC7CCCCCCACA?5A5<

5. You've decided that you want to make a seperate file of the reads to BLAST them at NCBI to make sure they belong to the species that you sequenced. However, your blast program is written to accept FASTA files rather than FASTQ files (FASTA files only contain the header line above the read, and the read itself). You will need to make a 'FASTA' file from each FASTQ file. Before you make the new files, pipe the output to a command that allows you to see just the first lines of the output. (5 points)

grep --no-group-separator -A1 ^@SRR SRR097977.fastq | head

6. Redirect the output of your command (command in 6 that is converting the format of the FASTQ into FASTA) into new files. Give the new file the same names, but uses the '.fasta' extension rather than the '.fastq' extension of the original file name. (5 points)

grep --no-group-separator -A1 ^@SRR SRR097977.fastq > SRR097977.fasta

grep --no-group-separator -A1 ^@SRR SRR098026.fastq > SRR098026.fasta

7. How many reads have 15 or more uncalled bases (NNNNNNNNNNNNNNN) in both samples? Count the number of reads in both WITHOUT making a new file. (4 points)

grep NNNNNNNNNNNNNNN SRR097977.fastq | wc -l (0 Lines)

8. Make a new directory called 'to_blast' in your current directory. Then, move the two fasta files into this new 'to_blast' directory (4 points)

mkdir to_blast

mv *.fasta to_blast

9. Without changing directories, what command could you use to confirm that the files made it into the 'to_blast' folder. (2 points)

ls /home/users/lhi1001/gen711-811/analysis/to_blast/

10. What is the 100th line in the Sample1.fasta file? (hint: the 'head' command is one way to do this- but you may need to specify an option) (2 points)

 head -n 100 SRR097977.fasta (GCGGAGCTGGTGATTGGCGAACTGCTGCTGCTATTT)

11. Run md5sum on Sample1.fasta (md5sum Sample1.fasta). Then, run it again, but redirect the output to a new file called 'my_md5sums.txt'.  (2 points)

md5sum SRR097977.fasta

md5sum SRR097977.fasta > my_md5sums.txt

12. Next, run the md5sum command on Sample2.fasta and add it the the end of 'my_md5sums.txt'. (2 points)

md5sum SRR098026.fasta

md5sum SRR098026.fasta >> my_md5sums.txt

13. Lastly, add your name to the end of 'my_md5sums.txt' file. (2 points)

echo Luke_Insana >> my_md5sums.txt



14. Use an absolute path to change your current working directory to the 'prac_exam' directory that you just cloned (2 points).

cd /home/users/lhi1001/prac_exam_2026/


15. From 'prac_exam' directory, make the following directory structure in a single command: `data/untrimmed_fastq` (2 points, -1 point if you need to use 2 commands for this. Hint: There is a flag/option that lets you create nested directories all at once.)

mkdir data
mkdir untrimmed_fastq


16. Copy the two fastq files in the `/tmp/Gen711-811_data` directly into your `untrimmed_fastq` directory without changing your current directory. (2 points, partial credit if you need to change directories first. Multiple correct answers)

cp /tmp/Gen711-811_data/SRR*.fastq.gz /home/users/lhi1001/prac_exam_2026//untrimmed_fastq/

  
17. List all the hidden files in this repo. Paste the command below (2 points) -1 point

ls -a

18. Use a relative path to change your current working directory to the `untrimmed_fastq` directory. (2 points)

cd untrimmed_fastq/


19. These are paired-end FASTQ files from an *E. coli* long-term evolution experiment. To confirm the files look ok, view one of them and paste the top 4 lines below. (4 points, Hint: These files are gzip-compressed. Multiple correct answers)

@SRR2584863.1 HWI-ST957:244:H73TDADXX:1:1101:4712:2181/2
GGCGACATTACTGACCCGCNNNNNNNNNNNNNNNNNNNCGACNNNNNNNNNNNNNNNNNCCTGATNNNNNNNNNNNNNNNTCAGNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
+
<<<??@??@??@@?@@??@###################################################################################################################################


20. How large (file size) are the two uncompressed fastq files? Use a single command with appropriate options to show the file sizes in a human-readable format (e.g., MB). Paste the command and output below. (2 points) -1 point

ls --size SRR258486*_2.fastq

557864 SRR2584863_2.fastq  995140 SRR2584866_2.fastq (??)



21. For each fastq, how many quality score lines have the '@' symbol in them? To answer this, use one line of piped bash commands for each fastq, and the output should be a single number.(2 points)

grep --no-group-separator ^@SRR SRR2584863_2.fastq | wc -l (1553259 qualtiy score lines)

grep --no-group-separator ^@SRR SRR2584866_2.fastq | wc -l (2768398 qualtiy score lines)


22. How many reads have 15 or more uncalled bases (`NNNNNNNNNNNNNNN`) in `SRR2584863_1.fastq`? Count WITHOUT making a new file (4 points)

grep NNNNNNNNNNNNNNN SRR2584863_2.fastq | wc -l

Answer: 3015


23. Make a single fasta file from the two fastqs using the reads found in the question above, and their respective info lines. Name the new file 'badreads.fasta' in the 'untrimmed_fastq' directory.  (4 points)

Hint: the first 4 lines of badreads.fasta should look similar (but maybe not exactly) to this:
```
@SRR2584863.1 HWI-ST957:244:H73TDADXX:1:1101:4712:2181/2
GGCGACATTACTGACCCGCNNNNNNNNNNNNNNNNNNNCGACNNNNNNNNNNNNNNNNNCCTGATNNNNNNNNNNNNNNNTCAGNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
@SRR2584863.2 HWI-ST957:244:H73TDADXX:1:1101:8571:2191/2
TCCCCGGAGTCAGCAGGGTGNNNNNNNNNNNNNNNNNATACATNNNNNNNNNNNNNNNGTTTTTGNNNNNNNNNNNNNNGCTGTCNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
```
grep --no-group-separator -A1 ^@SRR SRR2584863_2.fastq > badreads.fasta

grep --no-group-separator -A1 ^@SRR SRR2584866_2.fastq >> badreads.fasta

Mine .fasta file format

@SRR2584863.1 HWI-ST957:244:H73TDADXX:1:1101:4712:2181/2
GGCGACATTACTGACCCGCNNNNNNNNNNNNNNNNNNNCGACNNNNNNNNNNNNNNNNNCCTGATNNNNNNNNNNNNNNNTCAGNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN
@SRR2584863.2 HWI-ST957:244:H73TDADXX:1:1101:8571:2191/2
TCCCCGGAGTCAGCAGGGTGNNNNNNNNNNNNNNNNNATACATNNNNNNNNNNNNNNNGTTTTTGNNNNNNNNNNNNNNGCTGTCNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN

24. Activate the conda 'genomics' environment that contains `fastqc` and confirm where `fastqc` is installed. Paste the command and its output below. (2 points)

conda activate genomics

fastqc SRR2584863_2.fastq

null
Started analysis of SRR2584863_2.fastq
Approx 5% complete for SRR2584863_2.fastq
Approx 10% complete for SRR2584863_2.fastq
Approx 15% complete for SRR2584863_2.fastq
Approx 20% complete for SRR2584863_2.fastq
Approx 25% complete for SRR2584863_2.fastq
Approx 30% complete for SRR2584863_2.fastq
Approx 35% complete for SRR2584863_2.fastq
Approx 40% complete for SRR2584863_2.fastq
Approx 45% complete for SRR2584863_2.fastq
Approx 50% complete for SRR2584863_2.fastq
Approx 55% complete for SRR2584863_2.fastq
Approx 60% complete for SRR2584863_2.fastq
Approx 65% complete for SRR2584863_2.fastq
Approx 70% complete for SRR2584863_2.fastq
Approx 75% complete for SRR2584863_2.fastq
Approx 80% complete for SRR2584863_2.fastq
Approx 85% complete for SRR2584863_2.fastq
Approx 90% complete for SRR2584863_2.fastq
Approx 95% complete for SRR2584863_2.fastq
Analysis complete for SRR2584863_2.fastq

fastqc SRR2584866_2.fastq

null
Started analysis of SRR2584866_2.fastq
Approx 5% complete for SRR2584866_2.fastq
Approx 10% complete for SRR2584866_2.fastq
Approx 15% complete for SRR2584866_2.fastq
Approx 20% complete for SRR2584866_2.fastq
Approx 25% complete for SRR2584866_2.fastq
Approx 30% complete for SRR2584866_2.fastq
Approx 35% complete for SRR2584866_2.fastq
Approx 40% complete for SRR2584866_2.fastq
Approx 45% complete for SRR2584866_2.fastq
Approx 50% complete for SRR2584866_2.fastq
Approx 55% complete for SRR2584866_2.fastq
Approx 60% complete for SRR2584866_2.fastq
Approx 65% complete for SRR2584866_2.fastq
Approx 70% complete for SRR2584866_2.fastq
Approx 75% complete for SRR2584866_2.fastq
Approx 80% complete for SRR2584866_2.fastq
Approx 85% complete for SRR2584866_2.fastq
Approx 90% complete for SRR2584866_2.fastq
Approx 95% complete for SRR2584866_2.fastq
Analysis complete for SRR2584866_2.fastq


25. Run `fastqc` on `SRR2584863_1.fastq`. Then, create a `results/fastqc_untrimmed_reads` directory and move both the `.zip` and `.html` output files into it — all without leaving your `untrimmed_fastq` directory. Paste all commands used. (4 points)

mkdir fastqc_untrimmed_reads

mv *_fastqc.html fastqc_untrimmed_reads

mv *_fastqc.zip fastqc_untrimmed_reads


26. Without changing directories, what is the 100th line of the file `SRR2584863_1.trim.fastq` in your `trimmed_fastq` directory? (2 points)

head -100 SRR2584863_2.fastq

100th line: ::>CAA>>B>><55:(:@8?B###########


27. Run `md5sum` on `SRR2584863_1.fastq`. Then run it again, redirecting the output to a new file called `my_md5sums.txt`. Next, run `md5sum` on `SRR2584863_2.fastq` and **append** it to `my_md5sums.txt`. Finally, append your name to the end of `my_md5sums.txt`. Paste all commands used. (4 points)

md5sum SRR2584863_2.fastq

md5sum SRR2584863_2.fastq > my_md5sums.txt

md5sum SRR2584866_2.fastq >> my_md5sums.txt