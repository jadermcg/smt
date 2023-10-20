# Sparse Motif Tree (SMT)

The Sparse Motif Tree (`SMT`) is an innovative data structure designed to store and count k-mers efficiently in large volumes of genomic data. `SMT` optimizes memory usage and computation time, enabling rapid and accurate analysis of DNA and RNA sequences. Detecting conserved motifs and patterns within sequences is crucial for understanding gene functions and regulations and for identifying functional and structural elements in the genome.

`SMT` is constructed using a sparse matrix that stores the k-mers and their respective nodes. The process of creating the `SMT` is performed by the `createSMT` algorithm, which inserts the k-mers into the matrix, ensuring time and space optimization.

The `ksearch` algorithm performs exact k-mer search in the SMT, checking whether the queried k-mer is present in the structure. The exact search is performed in constant time, making SMT an efficient tool for large-scale analyses.

The `kIUPACscan` algorithm is a specialized search function designed to identify and count patterns specified in IUPAC format within a Sparse Motif Tree (SMT). The IUPAC format is a standard way of representing nucleic acid sequences, making this algorithm particularly useful for bioinformatics and the study of genetic sequences. When an IUPAC pattern is provided to the function, it traverses the SMT to identify all instances of this pattern. The function then returns all the kmers that match the IUPAC pattern along with their counts, stored in a map where each kmer is mapped to its respective count. This provides a concise, high-level summary of all locations in the SMT where the pattern of interest occurs, as well as how frequently each associated kmer is found.

The `kdive` algorithm is responsible for approximate search in the SMT, allowing for the discovery of k-mers with up to `d` uniformly distributed mutations across their bases. The approximate search is performed in linear time, making the analysis of variations within DNA and RNA sequences fast and accurate.

The `kwildDelete` algorithm removes k-mers from the SMT and their surroundings, assisting in the identification of conserved regions and the analysis of variations. The removal is performed efficiently, ensuring that the SMT is updated correctly.

Finally, the `ktops` algorithm performs the extraction of enriched k-mers from the SMT. The extraction process is efficient and enables the identification of recurring patterns and conserved regions within sequences.

In addition to the aforementioned algorithms, the SMT package also includes the following functions:

- `ktop`: Returns the best kmer from SMT.
- `sparsity_level`: Returns the sparsity level of the SMT.
- `kdelete`: Performs the exact removal of a kmer.

By combining these algorithms, the SMT offers an efficient and robust solution for genomic data analysis, contributing to a better understanding of gene functions and regulations and assisting in the identification of functional and structural elements in the genome.

To see the pseudocode of the main algorithms, click on the links below:
- [createSMT Pseudocode](createSMT_pseudocode.md)
- [ksearch Pseudocode](KSearch_pseudocode.md)
- [kIUPACscan Pseudocode](IUPACSearch_pseudocode.md)
- [kdive Pseudocode](dDFS_pseudocode.md)
- [kwildDelete Pseudocode](sDLT_pseudocode.md)
- [ktops Pseudocode](getBestKmers_pseudocode.md)
