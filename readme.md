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

The data I will use are (my own data/ data publicly available at YYY/ simulations)

## Methods
This project consists of two main branches. The first branch uses protein sequence data to look at magnesium ion channels in Homo sapiens. Protein data is superior to DNA and RNA data in this instance because the channels operate at the protein level. We do not need to think about the relative importance of coding and noncoding DNA regions. Moreover, amino acids convey information in fewer letters than their corresponding DNA codons and avoid dealing with the degeneracy of the DNA code.

I began with a series of accession numbers pertaining to protein sequences involved in magnesium trasnport -- both in humans and other organisms. I also include acession numbers pertaining to epithelial sodium channel family as a control and the ribosomal protein as an outgroup. Using a procedure similar to the hydroilina exercise, I used ProteinBlast to find the corresponding protein sequence.

    sed -E 's/>.+\| ([a-zA-Z]+) ([a-zA-Z]+)[\. ].+/>\1_\2/g' mg.raw.fasta > mg.fasta



A second branch of the project uses morphological data as a proof of principle to analyze ion channel phylogeny. Because of the precision and abundance of sequence data, it is the dominant method of phylogenetic analysis, especially when protein structures have not been fully resolved. Yet the mantra of biology that structure determines function rings true. A shortcoming of protein sequence data is that it only allows us to examine the primary structure of the ion channels--the order of amino acids. 
Amino acid form secondary, tertiary and quaternary structures in which the various residues and subunits interact. Two different amino acids may produce near-identical three-dimensional structure or a single residue substitution could contort the entire structure.

The tools I used were... See analysis files at (links to analysis files).

## Results


The tree in Figure 1...

## Discussion

These results indicate...

The biggest difficulty in implementing these analyses was...
A major difficulty in completing the project was my limited understanding of programming. In my project, I sought to do what I thought of as an interesting application of phylogentics and the topics we have discussed without thinking too much about feasibility of the computer model or my own limited proficiency in the area. This manifested itself in several challenges in implementing the programming aspect of the project. The project took me much longer than expected to complete. I ran into several hiccups in terms of syntax and execution. For example, there seemed to be a problem with loading my .nex file into the RevBayes program. I initially thought there was a syntax error in the command to input the discrete character data or that it had not been properly formatted for protein data. It turned out that the .nex file converted in Mesquite was noncompatable with RevBayes. By using an online .fasta to .nex conversion tool (http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) instead, I was able to create a compatable .nex file.

If I did these analyses again, I would...

## References
(Payendeh et al, 2013) http://www.sciencedirect.com/science/article/pii/S0005273613002794?np=y

(Hanukoglu and Hanukoglu, 2016) http://www.sciencedirect.com/science/article/pii/S0378111915015735

