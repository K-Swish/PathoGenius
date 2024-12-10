# PathoGenius
A Filoviridae Ebolavirus Genome database


Find all other info here: https://k-swish.github.io/PathoGenius/

## Instalation:
To install, please ensure you already have a functioning Apache2 web server. 

Apache2 web servers serve files from within a root directory. For a normal linux installation, the folder should be /var/www or /var/www/html, whereas when you install on macOS using brew it will likely be in /opt/homebrew/var/www (for M1) or /usr/local/var/www (for Intel). Set APACHE_ROOT to the path to your root directory.
```
export APACHE_ROOT='/path/to/rootdir'
```
Then, make a temporary directory as a staging area.
```
mkdir ~/tmp
cd ~/tmp
```
Download and copy over jbrowse2 into your root directory and set the owner to the curent use (you)
```
jbrowse create output_folder
sudo mv output_folder $APACHE_ROOT/jbrowse2
sudo chown -R $(whoami) $APACHE_ROOT/jbrowse2
```
Next, download the genome assemblies, including the viral genomes for the 6 species in Ebolavirus and their respective genome annotations. While still in your temporary directory, simply copy and run the following code:
```
export FASTA_URL_BOMBALI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/003/505/815/GCF_003505815.1_ASM350581v1/GCF_003505815.1_ASM350581v1_genomic.fna.gz
wget $FASTA_URL_BOMBALI
gunzip GCF_003505815.1_ASM350581v1_genomic.fna.gz
mv GCF_003505815.1_ASM350581v1_genomic.fna Bombali_Virus.fa
samtools faidx Bombali_Virus.fa
jbrowse add-assembly Bombali_Virus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_BOMBALI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/003/505/815/GCF_003505815.1_ASM350581v1/GCF_003505815.1_ASM350581v1_genomic.gff.gz
wget $GFF_URL_BOMBALI
gunzip GCF_003505815.1_ASM350581v1_genomic.gff.gz
mv GCF_003505815.1_ASM350581v1_genomic.gff Bombali_Virus.gff
jbrowse sort-gff Bombali_Virus.gff > Bombali_Virus_sorted.gff
bgzip Bombali_Virus_sorted.gff
tabix Bombali_Virus_sorted.gff.gz
jbrowse add-track Bombali_Virus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Bombali_Virus
jbrowse text-index --out $APACHE_ROOT/jbrowse2


export FASTA_URL_BUNDI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/889/155/GCF_000889155.1_ViralProj51245/GCF_000889155.1_ViralProj51245_genomic.fna.gz
wget $FASTA_URL_BUNDI
gunzip GCF_000889155.1_ViralProj51245_genomic.fna.gz
mv GCF_000889155.1_ViralProj51245_genomic.fna Bundibugyo_Virus.fa
samtools faidx Bundibugyo_Virus.fa
jbrowse add-assembly Bundibugyo_Virus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_BUNDI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/889/155/GCF_000889155.1_ViralProj51245/GCF_000889155.1_ViralProj51245_genomic.gff.gz
wget $GFF_URL_BUNDI
gunzip GCF_000889155.1_ViralProj51245_genomic.gff.gz
mv GCF_000889155.1_ViralProj51245_genomic.gff Bundibugyo_Virus.gff
jbrowse sort-gff Bundibugyo_Virus.gff > Bundibugyo_Virus_sorted.gff
bgzip Bundibugyo_Virus_sorted.gff
tabix Bundibugyo_Virus_sorted.gff.gz
jbrowse add-track Bundibugyo_Virus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Bundibugyo_Virus
jbrowse text-index --out $APACHE_ROOT/jbrowse2



export FASTA_URL_RESTON=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/854/085/GCF_000854085.1_ViralProj15006/GCF_000854085.1_ViralProj15006_genomic.fna.gz
wget $FASTA_URL_RESTON
gunzip GCF_000854085.1_ViralProj15006_genomic.fna.gz
mv GCF_000854085.1_ViralProj15006_genomic.fna Reston_Virus.fa
samtools faidx Reston_Virus.fa
jbrowse add-assembly Reston_Virus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_RESTON=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/854/085/GCF_000854085.1_ViralProj15006/GCF_000854085.1_ViralProj15006_genomic.gff.gz
wget $GFF_URL_RESTON
gunzip GCF_000854085.1_ViralProj15006_genomic.gff.gz
mv GCF_000854085.1_ViralProj15006_genomic.gff Reston_Virus.gff
jbrowse sort-gff Reston_Virus.gff > Reston_Virus_sorted.gff
bgzip Reston_Virus_sorted.gff
tabix Reston_Virus_sorted.gff.gz
jbrowse add-track Reston_Virus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Reston_Virus
jbrowse text-index --out $APACHE_ROOT/jbrowse2



export FASTA_URL_SUDAN=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/855/585/GCF_000855585.1_ViralProj15012/GCF_000855585.1_ViralProj15012_genomic.fna.gz
wget $FASTA_URL_SUDAN
gunzip GCF_000855585.1_ViralProj15012_genomic.fna.gz
mv GCF_000855585.1_ViralProj15012_genomic.fna Sudan_Virus.fa
samtools faidx Sudan_Virus.fa
jbrowse add-assembly Sudan_Virus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_SUDAN=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/855/585/GCF_000855585.1_ViralProj15012/GCF_000855585.1_ViralProj15012_genomic.gff.gz
wget $GFF_URL_SUDAN
gunzip GCF_000855585.1_ViralProj15012_genomic.gff.gz
mv GCF_000855585.1_ViralProj15012_genomic.gff Sudan_Virus.gff
jbrowse sort-gff Sudan_Virus.gff > Sudan_Virus_sorted.gff
bgzip Sudan_Virus_sorted.gff
tabix Sudan_Virus_sorted.gff.gz
jbrowse add-track Sudan_Virus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Sudan_Virus
jbrowse text-index --out $APACHE_ROOT/jbrowse2



export FASTA_URL_TAI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/888/475/GCF_000888475.1_ViralProj51257/GCF_000888475.1_ViralProj51257_genomic.fna.gz
wget $FASTA_URL_TAI
gunzip GCF_000888475.1_ViralProj51257_genomic.fna.gz
mv GCF_000888475.1_ViralProj51257_genomic.fna Tai_Forest_Virus.fa
samtools faidx Tai_Forest_Virus.fa
jbrowse add-assembly Tai_Forest_Virus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_TAI=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/888/475/GCF_000888475.1_ViralProj51257/GCF_000888475.1_ViralProj51257_genomic.gff.gz
wget $GFF_URL_TAI
gunzip GCF_000888475.1_ViralProj51257_genomic.gff.gz
mv GCF_000888475.1_ViralProj51257_genomic.gff Tai_Forest_Virus.gff
jbrowse sort-gff Tai_Forest_Virus.gff > Tai_Forest_Virus_sorted.gff
bgzip Tai_Forest_Virus_sorted.gff
tabix Tai_Forest_Virus_sorted.gff.gz
jbrowse add-track Tai_Forest_Virus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Tai_Forest_Virus
jbrowse text-index --out $APACHE_ROOT/jbrowse2



export FASTA_URL_ZAIRE=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz
wget $FASTA_URL_ZAIRE
gunzip GCF_000848505.1_ViralProj14703_genomic.fna.gz
mv GCF_000848505.1_ViralProj14703_genomic.fna Zaire_Ebolavirus.fa
samtools faidx Zaire_Ebolavirus.fa
jbrowse add-assembly Zaire_Ebolavirus.fa --out $APACHE_ROOT/jbrowse2 --load copy

export GFF_URL_ZAIRE=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz
wget $GFF_URL_ZAIRE
gunzip GCF_000848505.1_ViralProj14703_genomic.gff.gz
mv GCF_000848505.1_ViralProj14703_genomic.gff Zaire_Ebolavirus.gff
jbrowse sort-gff Zaire_Ebolavirus.gff > Zaire_Ebolavirus_sorted.gff
bgzip Zaire_Ebolavirus_sorted.gff
tabix Zaire_Ebolavirus_sorted.gff.gz
jbrowse add-track Zaire_Ebolavirus_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames Zaire_Ebolavirus
jbrowse text-index --out $APACHE_ROOT/jbrowse2
```
Now that you've scrolled all the way down here, launch JBrowse2 vis your local Apache2 server! For local hosting, the url will be http://localhost:8080/ (Mac) or http://XX.XXX.XXX.XX:8080/ (Linux/WLS/AWS), where Xs are replaced with the appropriate IP address from the WSL steps below.

## Configuration
Congrats, you have a functioning JBrowse2 instance! Your JBrowse2 instance will be empty when you start. Do not fret! Click on "Linear Genome View," and select whichever annotated and indexted Ebolavirus genome you want to look at first. Then select "OPEN TRACK SELECTOR" and select the .gff track. Voila!

To open tabular genome/proteome analysis (CSV files), multi sequence alignments (MSAs), phylogenetic/phyloproteomic trees (Newick Trees), 3D Protein structures (.cif files) start by going to "TOOLS" --> "Plugin store" and download the "MsaView" and "Protein3d" plugins. 

### Tabular genome/proteome analysis (CSV files)
For these, simply go to "ADD" --> "Spreadsheet view" and load in your csv file. I have provided two in https://github.com/K-Swish/PathoGenius/tree/main/downloadables:
1. ebov_gp_regions.csv
2. percent_identity_matrix_nuc.csv

The former is an alignment of the ebolaviruses glycoproteins (GPs) which are the only cytosolcially exposed protein on their capsid's surface! It lists the entropy for each AA space in the aslignment, if the average entropy of the 3 nearest AA in that region is low or high (conserved or not), and if it is exposed to the cytosol (not the whole GP is). Use this to identify regions of theraputic interest!
The latter is a percent identity matrix comparing each ebolavirus genome with themselves.

### Multi sequence alignments (MSAs) and Phylogenetic/phyloproteomic trees (Newick Trees)
For these, go to "ADD" --> "Multiple sequence alignment view" and select a tree and MSA file. I have given you two pairs:
1. ebov_genomes_msa_clustral.txt and ebov_genomes_newick_tree.txt
2. ebov_gp_msa_clustral.txt and ebov_gp_newick_tree.txt

These are MSAs for the viral genomes and for specifically their GPs respectively.

### 3D Protein structures
These are tricky, sorry. Hover over any coding seuqence in a linear genome view. Right click and select "Launch protein view". Select "OPEN FILE MANUALLY" and imput either the Zaire ebolavirus GP (Zaire_GP.cif) or the Bundibugyo virus GP (Bundibugyo_GP.cif), and click "LAUNCH 3-D PROTEIN STRUCTURE VIEW". Click the wrench on the right sidebar, and select the already-visible "Apply" button under "Download Structure". Now under "State Tree" (the graph-shaped item on the left sidebar), click "Assembly" --> "Apply Action" --> "3D Representation" and click the new "Apply" button". There you go! You can also now use "Quick Styles" on the right to change the structure's representation, but you're done!
