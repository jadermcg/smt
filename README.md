# Sparse Motif Tree (SMT)

The Sparse Motif Tree (`SMT`) is an innovative C++/Linux framework designed to store and count k-mers efficiently in large volumes of genomic data. `SMT` optimizes memory usage and computation time, enabling rapid and accurate analysis of DNA and RNA sequences. Detecting conserved motifs and patterns within sequences is crucial for understanding gene functions and regulations and for identifying functional and structural elements in the genome.

`SMT` is constructed using a sparse matrix that stores the k-mers and their respective nodes. The process of creating the `SMT` is performed by the `createSMT` algorithm, which inserts the k-mers into the matrix, ensuring time and space optimization.

The `ksearch` algorithm performs exact k-mer search in the `SMT`, checking whether the queried k-mer is present in the structure. The exact search is performed in constant time, making SMT an efficient tool for large-scale analyses.

The `KIUPACscan` is a specialized search function designed to identify and count patterns specified in IUPAC format within a `SMT` data structure. The IUPAC format is a standard way of representing nucleic acid sequences, making this algorithm particularly useful for bioinformatics and the study of genetic sequences. When an IUPAC pattern is provided to the function, it traverses the `SMT` to identify all instances of this pattern. The function then returns all the kmers that match the IUPAC pattern along with their counts, stored in a map where each kmer is mapped to its respective count. This provides a concise, high-level summary of all locations in the `SMT` where the pattern of interest occurs, as well as how frequently each associated kmer is found.

The `Kdive` is responsible for approximate search in the `SMT`, allowing for the discovery of k-mers with up to `d` uniformly distributed mutations across their bases. The approximate search is performed in linear time, making the analysis of variations within DNA and RNA sequences fast and accurate. This is particularly useful in discovering conserved motifs, in which the patterns are similar but not identical.

The `Hmap` was devised to swiftly extract a map containing all the kmers and their respective frequencies from the `SMT`. The efficiency and speed of `Hmap` are attributed to its direct execution on the `SMT` tree structure, which facilitates organized access and recovery of kmers and their counts. This approach leverages the hierarchical and organized nature of the `SMT`, allowing for efficient traversal of the tree to compile the kmer map. The synergy between the tree structure of the `SMT` and the efficient execution of `Hmap` results in a powerful tool that provides quick and precise extraction of the kmer map, thus facilitating subsequent genomic analyses.

The algorithm `KHmap` improves the capabilities of `Hmap`, allowing for the extraction of kmer maps for any value of `k` lesser or equal to `kmax`. This feature is particularly useful when the `SMT` has been constructed for a specific value of `k`, such as `k = 30`, for instance. In this case, `KHmap` can efficiently extract all corresponding maps for `k = 1, 2, 3, . . . , 30`, providing a flexibility that is a significant differential of the `SMT` in comparison to other related data structures. Although `KHmap` is slightly slower compared to `Hmap`, its ability to extract maps for a variety of values of `k` makes it a preferable choice whenever analysis for multiple values of `k` is required.

By combining these algorithms, the `SMT` offers an efficient and robust solution for genomic data analysis, contributing to a better understanding of gene functions and regulations and assisting in the identification of functional and structural elements in the genome.

# When to use SMT
`SMT` was built with the main objective of assisting in the analysis of biological motifs. However, it can be used in any situation in which it is necessary to count kmers or perform operations on kmers, such as knowing which are the most frequent or which are the most frequent considering a certain number of mutations.

# Getting Started
Follow the instructions below to be able to run SMT.

## Prerequisites
Before installing the SMT package, make sure you meet the following prerequisites:
