# Phylogenetic Biology - Final Project

## Guidelines - you can delete this section before submission

This repository is a stub for your final project. Fork it, develop your project, and submit it as a pull request. Edit/ delete the text in this readme as needed.

Some guidelines and tips:

- Use the stubs below to write up your final project. Alternatively, if you would like the writeup to be an executable document (with [knitr](http://yihui.name/knitr/), [jupytr](http://jupyter.org/), or other tools), you can create it as a separate file and put a link to it here in the readme.

- For information on formatting text files with markdown, see https://guides.github.com/features/mastering-markdown/ . You can use markdown to include images in this document by linking to files in the repository, eg `![GitHub Logo](/images/logo.png)`.

- The project must be entirely reproducible. In addition to the results, the repository must include all the data (or links to data) and code needed to reproduce the results.

- If you are working with unpublished data that you would prefer not to publicly share at this time, please contact me to discuss options. In most cases, the data can be anonymized in a way that putting them in a public repo does not compromise your other goals.

- Paste references (including urls) into the reference section, and cite them with the general format (Smith at al. 2003).

- Commit and push often as you work.

OK, here we go.

# Using Phylogeny to Understand Magnesium Ion Channels

## Introduction and Goals

The goal of my project is to examine magnesium transport in the human body using phylogeny by comparing human magnesium ion channels to other ion channel families and to other methods of magnesium transport in eukaryotes and prokaryotes. A guiding question is thus whether human magnesium ion channels share greater homology with other human ion channels or other magnesium transport mechanisms.
What is...?

The methods I will use to do this are...

The data I will use are publicly available protein sequence gathered from the NCBI database, specifically proteins related to magnesium and sodium transport.  

## Methods
This project consists of two main branches. The first branch uses protein sequence data to look at magnesium ion channels in Homo sapiens. Protein data is superior to DNA and RNA data in this instance because the channels operate at the protein level. We do not need to think about the relative importance of coding and noncoding DNA regions. Moreover, amino acids convey information in fewer letters than their corresponding DNA codons and avoid dealing with the degeneracy of the DNA code.

I began with a series of accession numbers pertaining to protein sequences involved in magnesium transport -- both in humans and other organisms. I also include accession numbers pertaining to epithelial sodium channel family as a control and the ribosomal protein as an outgroup. Using a procedure similar to the hydroilina exercise, I used ProteinBlast to find the corresponding protein sequence. I adjusted the resulting *.raw.fasta file to a *.fasta file by shortening the protein names by hand because many of the protein names were very similar and differed by only a single digit (as in the case of TRPM6 and TRPM7) or contained nonalphanumeric characters, namely parentheses and plus signs. The sed command was too blunt a tool to reformat the names, so it proved more efficient to do it manually.

I then used an online [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) and selected the protrein option to convert the *.fasta file *.nex file.

All of the analyses were performed using RevBayes using slightly modified versions of existing RevBayes model.

A second branch of the project uses morphological data as a proof of principle to analyze ion channel phylogeny. Because of the precision and abundance of sequence data, it is the dominant method of phylogenetic analysis, especially when protein structures have not been fully resolved. Yet the mantra of biology that structure determines function rings true. A shortcoming of protein sequence data is that it only allows us to examine the primary structure of the ion channels--the order of amino acids. 
Amino acid form secondary, tertiary and quaternary structures in which the various residues and subunits interact. Two different amino acids may produce near-identical three-dimensional structure or a single residue substitution could contort the entire structure.

The tools I used were... See analysis files at (links to analysis files).

## Results


The tree in Figure 1...

## Discussion

These results indicate...

The biggest difficulty in implementing these analyses was...
A major difficulty in completing the project was my limited understanding of programming. In my project, I sought to do what I thought of as an interesting application of phylogentics and the topics we have discussed without thinking too much about feasibility of the computer model or my own limited proficiency in the area. This manifested itself in several challenges in implementing the programming aspect of the project. The project took me much longer than expected to complete. I ran into several hiccups in terms of syntax and execution. For example, there seemed to be a problem with loading my .nex file into the RevBayes program. I initially thought there was a syntax error in the command to input the discrete character data or that it had not been properly formatted for protein data. It turned out that the .nex file converted in Mesquite was noncompatable with RevBayes. By using an online .fasta to .nex conversion [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) instead, I was able to create a compatable .nex file.

Another complication was that OSCAR couldn't process my analyses, requiring me to use my laptop computer instead. When I initially tried to run the JTT model analysis on OSCAR, the system initiated an error message that the program took up too much computing power. I subsequently reduced the number of iterations, which allowed the program to fully load and begin running, but the program paused midway through the run with the same error message. I therfore ran the program on my own machine, which ran slowly but with no error messages.

If I could do these analyses again, I would use a different, specialized version of the  JTT model. The in-program Jones function in RevBayes utilized in this project is based on the original [1992 paper](http://bioinformatics.oxfordjournals.org/content/8/3/275.short) that proposes a general protein matrix. A [1994 paper](http://onlinelibrary.wiley.com/doi/10.1016/0014-5793(94)80429-X/abstract) by the same authors offers a version of the JTT model specific to transmembrane protein, of which ion channels are a subtype. This second Jones model would have thus been more relevant to the analysis but I was not sure how to create a custom matrix function in RevBayes.
If I did these analyses again, I would...

## References
(Payendeh et al, 2013) http://www.sciencedirect.com/science/article/pii/S0005273613002794?np=y

(Hanukoglu and Hanukoglu, 2016) http://www.sciencedirect.com/science/article/pii/S0378111915015735

