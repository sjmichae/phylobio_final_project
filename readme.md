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

# Comparing Morphological and Protein Sequence Models of Ion Channel Phylogeny

## Introduction and Goals
The goal of my project is to compare a morphological model based on protein substructures with a standard protein sequence evolution model. To that ends, this project examine magnesium transport in the human body using phylogeny by comparing human magnesium ion channels to other ion channel families and to other methods of magnesium transport in eukaryotes and prokaryotes. A guiding question is thus whether human magnesium ion channels share greater homology with other human ion channels or other magnesium transport mechanisms.
What is...?

Magnesium ions channels hold an essential role in human cellular physiology, regulating bone development, cardiomiocyte activity and energy release in conjunction with ATP. Divalent magnesium ions are the smallest cations involved in cellular pathways when dehydrated and among the largest when hydrated. Magnesium ion channel structures are also less resolved than other ion channel families (namely ENaC/Deg) and fairly diverse. This project aims to examine magnesium ion channel phylogeny to better understand the protein evolution of ion channels.



The methods I will use to do this are...

The data I will use are publicly available protein sequences gathered from the NCBI database, specifically proteins linked to magnesium and sodium transport. I also used a data table of physical characteristics of ion channels, gathered from the published literature.

## Methods and Rationale
This project consists of two main branches. The first branch uses protein sequence data to look at magnesium and sodium ion channels. Protein data is superior to DNA and RNA data in this instance because the channels operate at the protein level. We do not need to think about the relative importance of coding and noncoding DNA regions. Moreover, amino acids convey information in fewer letters than their corresponding DNA codons and we can avoid dealing with the degeneracy of the DNA code.

I began with a series of accession numbers pertaining to protein sequences involved in magnesium transport -- both in humans and prokaryotes. I also included accession numbers pertaining to ENaC/Deg family of ion channels as a control and the ribosomal protein as an outgroup. Using a procedure similar to the hydroilina exercise, I used ProteinBlast to find the corresponding protein sequence. I adjusted the resulting *.raw.fasta file to a *.fasta file by shortening the protein names by hand because many of the protein names were very similar and differed by only a single digit (as in the case of TRPM6 and TRPM7) or contained nonalphanumeric characters, namely parentheses and plus signs. The sed command was too blunt a tool to reformat the names, so it proved more efficient to do it manually.

I then used an online [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) and selected the protein option to convert the *.fasta file *.nex file.

All of the analyses were performed in RevBayes using slightly modified versions of existing phylogenetic models. In my first analysis, I used the Jukes-Cantor program from the hydrolina project and modified the program so that it corresponded to amino acid data instead of nucleotide data and that there were 20 possible character states for the 20 amino acids. In the second analysis, I modified the program again using the Jones function to simulate the JTT model, which relies upon a matrix of amino acid evolution probabilities based on a large sample of proteins.

A second branch of the project uses morphological protein data as a proof of principle to analyze ion channel phylogeny. Because of the precision and abundance of sequence data, it is the dominant method of phylogenetic analysis, especially when protein structures have not been fully resolved. Yet the mantra of biology that structure determines function rings true. 

A shortcoming of protein sequence data is that it only allows us to examine the primary structure--the order of amino acids--of the ion channels or any other protein for that matter. Yet the mantra of biology that structure determines function rings true.
Amino acids form secondary, tertiary and quaternary structures in which the various residues and subunits interact. Two different polypeptide chains may produce near-identical three-dimensional structures or a single residue substitution could contort the entire structure. Protein evolution models tend to deal with this quandary by focusing on the relative rates of evolution between each amino acid pair. For instance, the Dayhoff matrix shows that a negatively-charged aspartate residue is more likely to be substituted for a negatively-charged glutamate residue than any other amino acid.

For my morphology data, I compiled a table of quantifiable physical characteristics of the ion channel such as the number of transmembrane domains, number of subunits and number of extracellular loops. All of this data was gathered from the available literature. An ion channel is an ideal choice for collecting morphological data becuase the it has identifiable molecular substructures.
Below is the full [table](https://github.com/sjmichae/phylobio_final_project/blob/master/ionchannelmorphologytable.xlsx):

Channel | Ions | Family | Organism | Ion Charge |	# Transmembrane domains per subunit |	# Subunits	| Total TMs	| -omeric |	#Extracellular SubDomains or Loops |	#Intracellular Loops or Subdomains
---|---|---|---|---|---|---|---|---|---|---
ASIC1 |	H + |	ENaC/Deg |	human |	1 |	2 |	3	| 6	| heteromer |	5	| 1
ASIC4	H +	ENaC/Deg	human	1	2	3	6	heteromer	5	1
ENaC beta	Na+	ENaC/Deg	human	1	2	3	6	heteromer	5	1
TRMP6	Mg 2+	TRP (transient receptor potetial)	human (kidney, intestine)	2	6	4	24	heteromer	3	2
TRPM6_X12	Mg 2+	TRP (transient receptor potetial)	human (kidney, intestine)	2	6	4	24	heteromer	3	2
TRPM7	Mg 2+, Ca 2+	TRP (transient receptor potetial)	human, universallly	2	6	4	24	heteromer	3	2
MgtE_Thermus	Mg 2+, also Co 2+	(related to SLC41A1)	Thermus thermophilus	2	5	2	10	homomer	2	2
MgtE_Myobacterium	Mg 2+, also Co 2+	(related to SLC41A1)	Myobacterium	2	5	2	10	homomer	2	2
MRS2	Mg 2+	(related to CorA)	human, mitocondrial	2	2	5	10	homomer	1	2
CorA	Mg 2+,  also  Co 2+, Ni 2+	CorA (related to MRS2)	Pantuea ananatis (bacteria)	2	2	5	10	homomer	5	1
SLC41A1	Mg 2+ out, Na+ in	(related to MgtE)	human	1, 2	5.5	2	11	homomer	1	1
ALR1	Mg 2+, also Ni, Mn, Zn, Co	(related to CorA)	human	2	2	5	10	homomer	2	1


I simplified the table by limiting the organism column to human or bacteria and removing references to specific locations of the human ion channels. I also removed the the familial column as it effectively served as a prior. 


The tools I used were... See analysis files at (links to analysis files).

## Results


The tree in Figure 1...

## Discussion

These results indicate...

It was surprising to find that the first two analyses resulted in broadly similar conclusions, having expected the modified Jukes-Cantor model to provide an unreliable tree.

One of the continuing puzzles of phylogenetics involves differentiating between convergent and homologous evolution as well as horizontal evolution.
MRS2, a human mitocondrial magnesium transporter is closely related to CorA, a bacterial magnesium transporter, as indicated by the JTT model tree and other research papers. CorA and MRS2 are considered to be homologous proteins.

The biggest difficulty in implementing these analyses was...
A major difficulty in completing the project was my limited understanding of programming. In my project, I sought to do what I thought of as an interesting application of phylogentics and the topics we have discussed without thinking too much about feasibility of the computer model or my own limited proficiency in the area. This manifested itself in several challenges in implementing the programming aspect of the project. The project took me much longer than expected to complete. I ran into several hiccups in terms of syntax and execution. For example, there seemed to be a problem with loading my .nex file into the RevBayes program. I initially thought there was a syntax error in the command to input the discrete character data or that it had not been properly formatted for protein data. It turned out that the .nex file converted in Mesquite was noncompatable with RevBayes. By using an online .fasta to .nex conversion [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) instead, I was able to create a compatable .nex file.



Another complication was that OSCAR couldn't process my analyses, requiring me to use my laptop computer instead. When I initially tried to run the JTT model analysis on OSCAR, the system initiated an error message that the program took up too much computing power. I subsequently reduced the number of iterations, which allowed the program to fully load and begin running, but the program paused midway through the run with the same error message. I therfore ran the program on my own machine, which ran slowly but with no error messages.

If I could do these analyses again, I would use a different, specialized version of the  JTT model. The in-program Jones function in RevBayes utilized in this project is based on the original [1992 paper](http://bioinformatics.oxfordjournals.org/content/8/3/275.short) that proposes a general protein matrix. A [1994 paper](http://onlinelibrary.wiley.com/doi/10.1016/0014-5793(94)80429-X/abstract) by the same authors offers a version of the JTT model specific to transmembrane protein, of which ion channels are a subtype. This second Jones model would have thus been more relevant to the analysis but I was not sure how to create a custom matrix function in RevBayes.

A morphological protein model could prove useful in cases of a longer evolutionary timespan, where relative amino acid evolution frequency is less important. It could also 


If I did these analyses again, I would...

## References
(Payendeh et al, 2013) http://www.sciencedirect.com/science/article/pii/S0005273613002794?np=y

(Hanukoglu and Hanukoglu, 2016) http://www.sciencedirect.com/science/article/pii/S0378111915015735
