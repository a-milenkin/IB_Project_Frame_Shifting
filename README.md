# Extracting the required data from the chelatase_db database
```bash

#Extracting all signals
mysql -u *user* -p*password* -e "select parent_id, data from fshifts_param;" chelatase_db > signals.txt

#Extracting all id and genus information
mysql -u *user* -p*password* -e "select id, org_id from seqs;" chelatase_db > seq_id.txt

mysql -u *user* -p*password* -e "select id, seq_id from fshifts;" chelatase_db > fshifts_id.txt

mysql -u *user* -p*password* -e "select id, genus from orgs;" chelatase_db > org_id_genus.txt

```

# Receiving sequences in fasta format for each genus
Use 'txt_to_fasta.ipynb' to convert the txt signal file to a fasta file.

To get fasta files for each genus separately, use 'Find_Bacteria_signals.ipynb'.

# Signal analysis
Alignment tool(mlocarna) - http://www.bioinf.uni-freiburg.de/Software/

Secondary structure predictor tool(RNAalifold) - http://rna.tbi.univie.ac.at/
```bash
#Signal alignment
mlocarna signals.fasta 

#Prediction of the secondary structure of signal RNA
RNAalifold --color --aln result.aln 

```
# Alignment ant secondary structure prediction examples
![Image alt](https://github.com/Alexoflife/chelatase_db_analysis/blob/main/Pseudomonas_cons_seq.png)
![Image alt](https://github.com/Alexoflife/chelatase_db_analysis/blob/main/Pseudomonas_SecStr.png)

# Interface task description

The database interface looks like this

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_home.PNG)

Let's open the tab with the list of organisms

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_main.PNG)

Now let's choose any organism. For example Delftia acidovorans SPH-1
So, we see some information about genes with frameshifing

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_1.PNG)

This table is not very informative. We will visualize it using special frameworks such as `DNA Features Viewer`.

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/Results.PNG)

Great! Now it is easier to perceive!
 
  
# References
1. I. Antonov. Two Cobalt Chelatase Subunits Can Be Generated from a Single
chlD Gene via Programed Frameshifting // Molecular Biology and Evolution, 2020, V. 37, p. 2268-2278.
2. S. Meydan et al. Programmed Ribosomal Frameshifting Generates a Copper Transporter and a Copper Chaperone from the Same Gene // Mol Cell. 2017, V. 65, p. 207-219.
3. I. Antonov et al. Identification of the nature of reading frame transitions observed in prokaryotic genomes // Nucleic Acids Res. 2013, V. 41, p. 6514–6530.








