# Corona Analysis

This project explores the genetic sequence of the Severe acute respiratory syndrome coronavirus 2 (SARS-CoV-2) isolate Wuhan-Hu-1, complete genome.

- **NCBI Source:** [NC_045512](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512)
- **Genome Size:** 29,903 base pairs ([Reference](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7539923/))

## Setup & Installation

To run the analysis locally, follow these steps:

1. **Create a Virtual Environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `.\venv\Scripts\activate`
   ```

2. **Install Dependencies:**

   ```bash
   pip install jupyter matplotlib biopython
   ```

3. **Launch Jupyter:**

   ```bash
   jupyter notebook
   ```

## Notebook Analysis (`corona.ipynb`)

The Jupyter notebook performs several computational biology tasks on the viral genome:

1.  **Sequence Cleaning:** The raw genome sequence is processed to remove metadata (numbers and whitespace), leaving only the nucleotide string (A, T, C, G).
2.  **Information Theory & Compression:**
    - The notebook uses `zlib` and `lzma` to compress the genome.
    - This relates to **[Kolmogorov complexity](https://en.wikipedia.org/wiki/Kolmogorov_complexity)**, measuring the algorithmic information content of the virus.
3.  **DNA to Protein Translation:**
    - A custom codon table is implemented to map DNA triplets to amino acids.
    - The sequence is translated into amino acid chains (`aa`) across different reading frames.
    - It includes checks for START and STOP codons to identify potential proteins.

### Genetic Code Reference

The translation process follows the standard genetic code:
![Codon Table](https://cdn.kastatic.org/ka-perseus-images/f5de6355003ee322782b26404ef0733a1d1a61b0.png)

_More info on [The Genetic Code](https://www.khanacademy.org/science/ap-biology/gene-expression-and-regulation/translation/a/the-genetic-code-discovery-and-properties)._

## Potential Next Steps

To further explore this genomic data, the following analysis can be implemented:

1.  **Identify Open Reading Frames (ORFs):**
    - Find all sequences that start with `START` (ATG) and end with `STOP` (TAA, TAG, TGA).
    - Filter for a minimum length (e.g., >100 amino acids) to identify potential functional proteins.
2.  **Visualize GC Content:**
    - Calculate the GC percentage (Guanine and Cytosine) across sliding windows (e.g., every 100 base pairs).
    - Plot the GC content to identify genomic regions with higher or lower stability.
3.  **Search for the Spike (S) Protein:**
    - Retrieve the known amino acid sequence for the SARS-CoV-2 Spike protein.
    - Use the `aa.find()` method to locate its position within the translated genome.
4.  **Comparative Genomics:**
    - Download the genome of other variants (e.g., Delta, Omicron) or related viruses (e.g., MERS, SARS-CoV).
    - Compare the compression (Kolmogorov complexity) and perform basic sequence alignments to identify mutations.
5.  **Integrate BioPython:**
    - Utilize the `BioPython` library for professional-grade sequence analysis, reading `.fasta` files, and connecting to the NCBI BLAST API.
