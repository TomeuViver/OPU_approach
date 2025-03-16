# **The OPU Approach to Diversity Metrics**

## **Description**
In this hands-on workshop, we will learn how to use the ARB program to cluster Amplicon Sequence Variants (ASVs) obtained from QIIME2 analysis into Operational Taxonomic Units (OPUs). Additionally, we will classify these OPUs taxonomically using the SILVA reference database.

By the end of this session, you will be able to:
- Integrate new sequences into the SILVA database.
- Align sequences within the ARB environment.
- Import sequences into a pre-established SILVA database.
- Identify Operational Taxonomic Units (OPUs).
- Obtain the phylogenetic assignment of OPUs.

---

## **1. Download and Prepare the SILVA Database**
The [SILVA database] (https://www.arb-silva.de/download/arb-files/) is commonly used for phylogenetic classification of ribosomal RNA sequences. We will use the **SILVA Release 138.2 Ref NR 99** as our reference.

###  **Visit the SILVA Database Webpage**
[https://www.arb-silva.de/download/arb-files/](https://www.arb-silva.de/download/arb-files/)

### **OPEN THE WORKING FOLDER**

Open the working folder:
```bash
cd /home/vmuser/Desktop/QIIME2
```
The file <span style="color:red;">SILVA_138.1_SSURef_NR99_CAME_3.arb</span> is the reduced SILVA file that we will use during the workshop.

---

## **ASV Representative Sequences**
The ASV representative sequences generated from QIIME2 are within the working directory:
```bash
ls -lh dna-sequences-rename.fasta
```
This file <span style="color:red;">dna-sequences-rename.fasta</span> contains the representative ASVs sequences that we will classify into OPUs.

Read the file:
```bash
less dna-sequences-rename.fasta
```

### **Step 5: Launch the ARB Program**
To start the ARB software, run:
```bash
arb
```
This will open the ARB graphical interface where we will perform sequence alignment, clustering, and taxonomic classification.

---

## **3. Clustering ASVs into OPUs and Exploring the Results**
After reconstructing OPUs, ARB will generate an output table named **OPUs_OTUs_relation.csv**. This file contains the ASVs assigned to OPUs along with their taxonomy based on the SILVA reference database.

### **Step 6: Merging ASV Data with OPU Assignments**
To integrate the taxonomic information with the ASV table, we will merge **table_otus_rename.csv** with **OPUs_OTUs_relation.csv**.

First, move to the Desktop:
```bash
cd /home/vmuser/Desktop/QIIME2
```

#### **Required files:**
```bash
ls table_otus_rename.csv
ls OPUs_OTUs_relation.csv .
```

#### **Format and merge the files:**
```bash
echo -e "OPUs\nASVs\tOPUs\tSILVA_taxonomy" | cat - OPUs_OTUs_relation.csv > OPUs_OTUs_relation_2.csv
paste table_otus_rename.csv OPUs_OTUs_relation_2.csv > Table_OPUs_Tax.csv
```
The final file **Table_OPUs_Tax.csv** now contains ASVs, their corresponding OPUs, and their taxonomic assignments. Open the file to explore the results!

---

## **4. Quantifying OPUs in Each Sample**
A custom script is available to calculate the total number of sequences per sample that belong to each OPU.

### **Step 7: Run the OPU Counting Script**
Execute the script with:
```bash
./script_OPUs_count.sh Table_OPUs_Tax.csv
```

### **Step 8: Examine the Output**
Once the script finishes running, open the output table:
```bash
column -t output_OPUs.csv | less
```
This file provides a summary of the distribution of OPUs across different samples.

---

## **Conclusion**
By following this workflow, we have successfully:
- Imported ASV sequences into ARB.
- Clustered sequences into OPUs.
- Assigned taxonomy using the SILVA database.
- Merged ASV and OPU classification results.
- Quantified the abundance of OPUs across samples.

This approach allows for a refined taxonomic classification beyond standard OTUs, improving our understanding of microbial diversity in environmental samples. 🎯

Let’s discuss any questions and explore the results together!
