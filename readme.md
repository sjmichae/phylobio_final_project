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
The goal of my project is to compare a morphological model based on protein substructures with a standard protein sequence evolution model. To that end, this project examines magnesium transport in the human body using phylogeny by comparing human magnesium ion channels to other ion channel families and to other methods of magnesium transport in eukaryotes and prokaryotes. Morphology is now predominantly used for studying fossils and to a lesser extent bone structures, but the same principles can be applied to protein ion channels with their quantifiable motifs.

Magnesium ions channels hold an essential role in human cellular physiology, regulating bone development, cardiomiocyte activity and energy release in conjunction with ATP. Divalent magnesium ions are the smallest cations involved in cellular pathways when dehydrated and among the largest when hydrated. Magnesium ion channel structures are also less resolved than other ion channel families (namely ENaC/Deg) and fairly diverse. This project aims to examine magnesium ion channel phylogeny to better understand the protein evolution of ion channels. A guiding question is thus whether a detailed protein morphology model can approach a sequence based likelihood model of the same protein.

The methods I will use are RevBayes analyses of protein sequence data using the modified Jukes-Cantor and JTT models and Raxml analyses of protein morphology data using an ordered and unordered model.

The data I will use are publicly available protein sequences gathered from the NCBI database, specifically proteins linked to magnesium and sodium transport. I also used a data table of physical characteristics of ion channels, gathered from the published literature.

## Methods and Rationale
This project consists of two main branches. The first branch uses protein sequence data to look at magnesium and sodium ion channels. Protein data is superior to DNA and RNA data in this instance because the channels operate at the protein level. We do not need to think about the relative importance of coding and noncoding DNA regions. Moreover, amino acids convey information in fewer letters than their corresponding DNA codons and we can avoid dealing with the degeneracy of the DNA code.

I began with a series of accession numbers pertaining to protein sequences involved in magnesium transport -- both in humans and prokaryotes. I also included accession numbers pertaining to ENaC/Deg family of ion channels as a control and the ribosomal protein as an outgroup. Using a procedure similar to the hydroidolina exercise, I used ProteinBlast to find the corresponding protein sequence. I adjusted the resulting *.raw.fasta file to a *.fasta file by shortening the protein names by hand because many of the protein names were very similar and differed by only a single digit (as in the case of TRPM6 and TRPM7) or contained nonalphanumeric characters, namely parentheses and plus signs. The sed command was too blunt a tool to reformat the names, so it proved more efficient to do it manually.

I then used an online [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) and selected the protein option to convert the *.fasta file *.nex file.

Both of these analyses were performed in RevBayes using slightly modified versions of existing phylogenetic models. In my first analysis, I used the [Jukes-Cantor program](JukesCantorProtein.Rev) from the hydroidolina project and modified the program so that it corresponded to amino acid data instead of nucleotide data and that there were 20 possible character states for the 20 amino acids. In the second analysis, I modified the program again using the [Jones function to simulate the JTT model](JTTProtein.Rev), which relies upon a matrix of amino acid evolution probabilities based on a large sample of proteins.

A second branch of the project uses morphological protein data as a proof of principle to analyze ion channel phylogeny. Because of the precision and abundance of sequence data, it is now the dominant method of phylogenetic analysis, especially when protein structures have not been fully resolved. Yet the mantra of biology that structure determines function rings true. 

A shortcoming of protein sequence data is that it only allows us to examine the primary structure--the order of amino acids--of the ion channels or any other protein for that matter. Amino acids form secondary, tertiary and quaternary structures in which the various residues and subunits interact. Two different polypeptide chains may produce near-identical three-dimensional structures or a single residue substitution could contort the entire structure. Protein evolution models tend to deal with this quandary by focusing on the relative rates of evolution between each amino acid pair. For instance, the Dayhoff matrix shows that a negatively-charged aspartate residue is more likely to be substituted for a negatively-charged glutamate residue than any other amino acid. Subsequent models of protein evolution such as JTT and WAG use different matrices, but still focus on the primary structure.

These methods represent a strong and reproducible model of amino acid evolution. But as [defenders](http://sysbio.oxfordjournals.org/content/53/4/653.full#ref-55) of morphological data would point out, sequence data can reach incorrect conclusions so the addition of morphology can result in a more complete tree. Admittedly, when discussing morphology, systematic biologists are thinking of morphology, they are generally speaking of fossils, bones or other macrostructures, not proteins or ion channels. An ion channel is still an ideal candidate for collecting morphological data because it has identifiable molecular motifs.

For my morphology data, I compiled a table of quantifiable physical characteristics of the ion channel such as the number of transmembrane domains, number of subunits and number of extracellular loops. All of this data was gathered from the available literature and complied in an Excel spreadhsheet. 
Attached is the full [table](https://github.com/sjmichae/phylobio_final_project/blob/master/ionchannelmorphologytable.xlsx).

I simplified the table by limiting the organism column to human or bacteria and removing references to specific locations of the human ion channels. I also removed the the familial column as it effectively served as a prior. The simplified table used for the matrix is below:

Channel|Ions|Organism|Ion Charge|# TM domains / subunit|# Subunits|Total TMs|-omer|#EL Loops|#IL Loops
:---|:---|:---|:---|:---|:---|:---|:---|:---|:---
ASIC1|H+|human|1|2|3|6|heteromer|5|1
ASIC4|H+|human|1|2|3|6|homomer|5|1
ENaC beta|Na+|human|1|2|3|6|heteromer|5|1
TRMP6|Mg2+|human|2|6|4|24|heteromer|3|2
TRPM6_X12|Mg2+|human|2|6|4|24|heteromer|3|2
TRPM7|Mg2+, Ca2+|human|2|6|4|24|heteromer|3|2
MgtE_Thermus|Mg2+, also Co2+|bacteria|2|5|2|10|homomer|2|2
MgtE_Myobac-terium|Mg2+, also Co2+|bacteria|2|5|2|10|homomer|2|2
MRS2|Mg2+|human|2|2|5|10|homomer|1|2
CorA|Mg2+,  also  Co2+, Ni2+|bacteria|2|2|5|10|homomer|5|1
SLC41A1|Mg2+ out, Na+ in|human|1, 2|5.5|2|11|homomer|1|1
ALR1|Mg2+, also Ni2+, Mn2+, Zn2+, Co2+|human|2|2|5|10|homomer|2|1

I converted the simplified Excel table to "Windows Formatted Text", a .txt file that preserved the line breaks and is readable for the user and the machine. I wrote a [sed](tablecommandsforshell.txt) command to convert the word variables to integral values for Raxml parsimony analysis. However, Raxml does not accept multiple character states to occur simultaneously in the same locus. It was therefore simpler to manually change the loci with multiple simultaneous character states (ion name, ion charge) to multiple binary loci.

Raxml allows for 32 character states in its multistate model with with double-digit numbers represented by letters. Since Raxml also requires that that the multistate characters must be used in "the order in which they are available," I created a new ion channel called FAKE consisting of the consecutive missing characters and later pruned FAKE from the output besttree file. Raxml also does not allow for identical sequences so the two MgtE and TRPM6 channels were consolidated. I ran two Raxml analyses, one with an [unordered multistate model](raxml_morph_unordered.sh) and one with an [ordered multistate model](raxml_multistateordered.sh) using the [The Excelis Lab code.](http://sco.h-its.org/exelixis/web/software/raxml/hands_on.html)

All of the output trees were analyzed in FigTree and the .logs were examined in Tracer.

## Results
All of the trees are displayed with the raw branch length as node labels.
Figure 1 displays the best tree for the amino acid version of the Jukes-Cantor model using sequence data.
![JC Model Best Tree](mg_JC_non_clock.trees_with_distance.png)

Figure 2 displays the best tree for the JTT model of protein evolution using sequence data.
![JTT Model Best Tree](mg_JTTmodel_non_clock_run_2_.tree_branch_length.png)

Figure 3 displays the best tree for the morphological data using an unordered maximum parsimony model.
![Morphology Regular Best Tree](RAxML_bestTree.morphtree.png)

Figure 4 displays the best tree for the morphological data using an ordered maximum parsimony model
![Morphology ORDERED Best Tree](RAxML_bestTree.trueorderedmorphtreepruned.png)

The tree in Figure 1...

## Discussion

At first glance, these results group all of the obvious homologues together: The two MgtE channels, the two TRPM6 channels and the ASIC channels are grouped together in the two RevBayes likelihood analyses. For the Raxml analyses, the MgtE channels from two genera of bacteria and the the two TRPM6 isoforms are structurally identical, at least according to the morphological data used and thus appear on the same node. All of the analyses also group the H+ ASIC channels with ENaC (epthithelial Na+ channels), which are homologous members of the well-defined ENaC/Deg superfamily. TRPM6 is grouped TRPM7 as both are homologous members of the transient receptor protein superfamily. 

It was surprising to find that the first two analyses resulted in broadly similar conclusions, having expected the modified Jukes-Cantor model to provide an unreliable tree. A significant difference however is the relative grouping of CorA and MgtE, each of which are the eponymous members of distinct magnesium ion channel families. The CorA family includes MRS2 and ALR1, while the MgtE family includes SLC41A1. In the Jukes-Cantor model, CorA and MgtE are grouped closely together though they not homologues. The JTT model is an improvement with SLC41A1 a short evolutionary distance from its homologue MgtE, though bizarrely ALR1 is placed in a monophyletic group between the ENaC/Deg superfamily and the MgtE family.

Among the morphological parsimony trees, the first unordered tree does group homologues corA and ALR1 together but groups SLC41A and MRS2 together, and also puts ASIC1 and ASIC4 on separate branches. The second ordered tree at least puts the ASIC channels on the same branch but produces a monophyly that includes the corA homolgues AND MgtE with SLC41A1 a long distance away from MgtE.

None of the trees produced offer what the literature would consider an accurate phylogeny of the ion channels, one with the corA homologues (corA, ALR1 and MRS2) and the MgtE homologues (MgtE and SLC41A1) each monophyletic. Some of the trees produce monophylies for TRPM and ENac/Deg families but none of the trees produce monophylies for corA nor MgtE. For the protein sequence data, it is somewhat surprising the trees do not coroborate consensus homologies, though perhaps a better model such as the JTT model specific to transmembrane proteins (see below) would have reflected the homologies. Protein evolution rates vary enough that the a more specialized model could make the difference. For the morphoogical trees, the deviation from the consensus homologies is indicative of the limitation of the characteristics used for this project. The two families of corA and MgtE differ in [secondary and tertiary characteristics](http://physiologyonline.physiology.org/content/23/5/275) such as a five intracellular domain in corA that form a funnel and two cystathionine beta-synthase intracellular domains in MgtE. The characteristics used for the project do capture some of the variation between the families such as 5 subunits in corA and its homologues compared to 2 subunits in MgtE and its homologues. In retrospect, if the latter character were overweighted the tree would more closely align withe the consensus.

One of the continuing puzzles of phylogenetics involves differentiating between convergent and homologous evolution as well as horizontal evolution. MRS2, a human mitocondrial magnesium transporter is closely related to corA, a bacterial magnesium transporter, with the proteins considered to be homologues. A plausible path for their evolution involves horizontal evolution in which the ancient bacteria that became a eukaryotic mitocondria contained the common ancestor of MRS2 and corA. It would be an interesting follow-up project to use a time-estimation model to see if the evolutionary timeline for MRS2 and corA corresponds to the endosymbiotic theory.

Looking at the trees also highlights one of the challenges of morphology: determining which data points to use. I chose characteristics  I thought were fundamental to an ion channel (number of subunits, number of transmembrane domains, number of extracellular domains) and that differentiated the channels (organism of channel, type of ion passing through). In so choosing, there is an inherent subjectivity. For ever characteristic I included, there were several I left out. There was also some ambiguity in compiling the data as the example of SLC41A1 illustrates. SLC41A1 is classified as a magnesium channel, though it is more precisely a magnesium/sodium exchanger, allowing for magnesium eflux and sodium influx. I therefore listed both ions in the table (Mg2+, Na+) as well as both charges (+2, +1). Some papers described SLC41A1 as having 10 transmembrane domains though a recent paper described the channel as a pseudodimer with 11 subunits. Which paper should I go with? I chose to use the more recent paper, listing SLC41A as having 11 transmembrane domains, 2 subunits and therefore 5.5 transmembrane domains per subunit. The Raxml model does not process fractional numbers, so I rounded down 5.5 to 5, an indication of some of the discretion inherent in using morphology.

This example also illustrated the potential for cherrypicking morphological characteristics to arrive at a particular result. I have no doubt I could reverse-engineer a tree that produced the desired groupings by focusing on specific characteristics shared by homologues and discretionary interpretation of ambiguous data. The solution to this temptation is to choose characteristics ex ante as I did, to base chosen characteristics on a well-defined set of parameters or to use an even larger set of characteristics.

A major difficulty in completing the project was my limited understanding of programming. In my project, I sought to do what I thought of as an interesting application of phylogentics and the topics we have discussed without thinking too much about feasibility of the computer model or my own limited proficiency in the area. This manifested itself in several challenges in implementing the programming aspect of the project. The project took me much longer than expected to complete. I ran into several hiccups in terms of syntax and execution. For example, there seemed to be a problem with loading my .nex file into the RevBayes program. I initially thought there was a syntax error in the command to input the discrete character data or that it had not been properly formatted for protein data. It turned out that the .nex file converted in Mesquite was incompatible with RevBayes. By using an online .fasta to .nex conversion [tool](http://sequenceconversion.bugaco.com/converter/biology/sequences/fasta_to_nexus.php) instead, I was able to create a compatible .nex file.

Another complication was that OSCAR couldn't process my analyses, requiring me to use my laptop computer instead. When I initially tried to run the JTT model analysis on OSCAR, the system initiated an error message that the program took up too much computing power. I subsequently reduced the number of iterations, which allowed the program to fully load and begin running, but the program paused midway through the run with the same error message. I therfore ran the program on my own machine, which ran slowly but with no error messages.

I also had difficulty troubleshooting with Raxml. Initially I tried to run the multistate model of Raxml on OSCAR, but soon realized the version of Raxml preloaded on OSCAR did not support that model, so I ran it on my laptop instead. I also tried to use a more complex Raxml code combining some of the functionality from the siphonophore assignment with the Exelis Lab code. The combined syntax did not run so I used the Exelis Lab multistate model. Once I had changed all of the double digit numbers to letters to accomodate the program(10 to A; 11 to B; 24 to O), it produced an error message that I had not used the characters in the order they are available. For the unordered model, I just changed the double digit numbers to unused single digit numbers as the distance between values did not matter. For the ordered model, I figured out I could add another ion channel called FAKE and add the missing consecutive characters for its data. I could then delete the FAKE output from the best tree. This workaround begged the question of why Raxml requires characters be used in the order they are available when its ordered model takes distance into account.

If I could do these analyses again, I would use a different, specialized version of the  JTT model. The in-program Jones function in RevBayes utilized in this project is based on the original [1992 paper](http://bioinformatics.oxfordjournals.org/content/8/3/275.short) that proposes a general protein matrix. A [1994 paper](http://onlinelibrary.wiley.com/doi/10.1016/0014-5793(94)80429-X/abstract) by the same authors offers a version of the JTT model specific to transmembrane protein, of which ion channels are a subtype. This second Jones model would have thus been more relevant to the analysis but I was not sure how to create a custom matrix function in RevBayes. For the morphology data, if I could do it again, I would add many more characteristics such as whether an ion channel is an exchanger or a uniport and remove certain criteria, namely whether the protein came from a human or bacteria, that have no structural basis. I also would have added an outgroup in addition to the ENaC/Deg channels.

A morphological protein model could prove useful in cases of a longer evolutionary timespan, where relative amino acid evolution frequency is less important. It could also prove useful in identifying protein orthologues across trees based on structural similarites regardless of the similarities of their sequences. For this project, the morphological trees do not seem any better than the likelihood based trees, but they offer a proof of principle that protein morphology trees can compare to protein sequence trees. If a larger dataset of morphology characteristics were to be used (or if I used "better" characteristics), we might produce trees that more closely resemble the true homology of the ion channels. Viewed in concert with sequence data, morphology data can provide a more robust assessment of phylogeny, even at the level of protein motifs.


## References

(Payendeh et al, 2013) http://www.sciencedirect.com/science/article/pii/S0005273613002794?np=y

(Hanukoglu and Hanukoglu, 2016) http://www.sciencedirect.com/science/article/pii/S0378111915015735

(Wiens) http://sysbio.oxfordjournals.org/content/53/4/653.full#ref-55


http://www.biochemj.org/content/412/3/469
http://www.sciencedirect.com.revproxy.brown.edu/science/article/pii/S0378111915015735
http://www.sciencedirect.com/science/article/pii/S0005273613002794
http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3503211/
http://www.biochemj.org/content/439/1/129.long
http://www.sciencedirect.com.revproxy.brown.edu/science/article/pii/S0925443907000841
http://www.jbc.org/content/280/45/37763.full.pdf
http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2630241/
http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3017111/
http://physiologyonline.physiology.org/content/23/5/275
http://ajpcell.physiology.org.revproxy.brown.edu/content/302/1/C318
http://www.sciencedirect.com.revproxy.brown.edu/science/article/pii/S096098221000566X
http://compbio.berkeley.edu/class/c246/Reading/dayhoff-1978-apss.pdf
