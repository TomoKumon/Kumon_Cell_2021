# Kumon_Cell_2021
Custom code for Kumon et al., Cell (2021)

How to obtain protein coding sequences from de novo assemblies
1. Obtain genome assemblies from NCBI BioProject database with accession number PRJNA669840 and save them under "assembly"
2. Obtain amino acid sequence (of a single exon) and save it under "query_sequence"
3. Go to the directory with GetDNfor, "assembly", "query_sequence", "ncbi-blast-2.10.1+", and "genes", and create a path.
	1. export PATH="${PATH}:./ncbi-blast-2.10.1+/bin"
	2. export PATH="${PATH}:."
4. Run GetDNfor. Gene name must be identical to the name of the query sequence.
	1. GetDNfor Cenpb
	2. If you have multiple genes, create a list of gene (e.g., your_genes.txt). 
	3. while read -r n ; do GetDNfor $n ; done < your_genes.txt
5. Import mouse reference sequence and de novo contigs in Geneious.
	1. For each genome, Align/Alignment — Map to Reference — OK
	2. Manually inspect alignment. 
	3. Go to table browser of UCSC. Obtain FASTA files for each CDS exon.
	4. Look for exon intron boundaries. Delete introns.
	5. DON'T FORGET TO DELETE REFERENCE SEQUENCE BEFORE EXPORT!!!
	6. Select Consensus — Extract.

How to run PAML and analyze results
1. Go to RAxML folder for each gene and run the following:
	1. raxmlHPC -f a -s Cenpb.phy -n tree -m PROTGAMMAAUTO -p 1985 -x 2020 -# 100 
	2. Copy RAxMLbestTree.tree to PAML folder. Rename Cenpb.tree. 

2. Go to PAML folder. Make sure the folder has RunPAML and changeme.ctl.
	1. Make sure the folder has:
		1. RunPAML
		2. changeme.ctl
		3. gene_name.phy
		4. gene_name.tree
	2. export PATH="${PATH}:."
	3. RunPAML Cenpb
3. gene_name_PAMLsummary.txt shows dN/dS and likelihood test results.
4. gene_name_mPAML is the PAML result file. Open it in any text editor. 
	1. Copy Mmd sequence. Open in SnapGene and translate into amino acid sequence.
	2. Compile UniProt reference amino acid sequence and PAML sequence.
	3. Open in Geneious. Align/Alignment. More Option penalty: 0 and 0
