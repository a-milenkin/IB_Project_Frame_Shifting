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







