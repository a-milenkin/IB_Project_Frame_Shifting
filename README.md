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

Running database-interface

Part of installation instructions was taken from [here](https://github.com/vanya-antonov/django_gtdb2/), but several items are fixed.
```bash
# Install blast
sudo apt-get install ncbi-blast+

git clone https://vanya-antonov@github.com/vanya-antonov/django_gtdb2
cd django_gtdb2

# scp ivan@10.0.1.254:~/_my/github/django_gtdb2/mysite/local_settings.py  mysite/
# - OR -
# scp -P 22194 ivan@83.149.211.146:~/_my/github/django_gtdb2/mysite/local_settings.py  mysite/

python3 -m venv  venv
source venv/bin/activate

# https://stackoverflow.com/a/44862371/310453
pip install --upgrade pip
pip install wheel

# On Ubuntu for mysqlclient:  https://stackoverflow.com/a/7475296/310453
sudo apt-get install libmysqlclient-dev

# On Ubuntu for numpy: https://stackoverflow.com/a/24892867/310453
sudo apt-get install python3.8-dev

cd django
pip install -r requirements.txt

# Copy and edit the local_settings.py
cp -v /home/gtdb/data/local_settings.py  mysite/

### Backend launch ###
# Run server with external access:
# ./manage.py runserver 0.0.0.0:8000 & 
# Run server at: http://127.0.0.1:8000/chelatase_db/
./manage.py runserver $  


### Frontend launch  ###
# Go to the folder 'frontend'
cd ../../
cd frontend/

npm install

#Build project
npm run serve

# Open server at: http://127.0.0.1:8000/chelatase_db/ 
# Enjoy it!

```


The database interface looks like this

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_home.PNG)

Let's open the tab with the list of organisms

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_main.PNG)

Now let's choose any organism. For example Delftia acidovorans SPH-1
So, we see some information about frame shift genes

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_1.PNG)

This table is not very informative. We will visualize it using special frameworks such as `DNA Features Viewer`.

![Image alt](https://github.com/a-milenkin/IB_Project_Frame_Shifting/blob/main/images/interface_results.PNG)

Great! Now it is easier to perceive!
 
This table visualization is much more useful and here's why:

The `chlD` gene can function in the composition with cobalt chelotase, synthesizing B12, and in the composition of magnesium chelotase, synthesizing chlorophyll. It turns out that `chlD` is a kind of" universal "gene - depending on where it is located, one can say in what biochemical pathway it participates.
 
For example: cobalt chelotase is encoded in the `cobN` gene. So if `chlH` is next to` cobN`, then the gene is involved in the biochemical pathway responsible for the synthesis of vitamin B12.

In order to make it easier to say where the `chlD` gene will take part, it is necessary to modify the entire database interface so that there are options for visualizing gene locations and also other types of visualizations. At the moment, some of the code has been written. 


Now all that remains is to integrate the developed code into the backend of the project written in the language - vue.js.
  
# References
1. I. Antonov. Two Cobalt Chelatase Subunits Can Be Generated from a Single
chlD Gene via Programed Frameshifting // Molecular Biology and Evolution, 2020, V. 37, p. 2268-2278.
2. S. Meydan et al. Programmed Ribosomal Frameshifting Generates a Copper Transporter and a Copper Chaperone from the Same Gene // Mol Cell. 2017, V. 65, p. 207-219.
3. I. Antonov et al. Identification of the nature of reading frame transitions observed in prokaryotic genomes // Nucleic Acids Res. 2013, V. 41, p. 6514–6530.








