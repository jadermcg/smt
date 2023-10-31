![smt](https://github.com/jadermcg/smt/blob/651edcee1e16a5a41bcf337d86024ff3df3a8161/smt.png)

# Kflex + Sparse Motif Tree: an efficient framework for counting and manipulating kmers.

The Sparse Motif Tree (`SMT`) is an innovative C++/Linux framework designed to store and count k-mers efficiently in large volumes of genomic data. `SMT` optimizes memory usage and computation time, enabling rapid and accurate analysis of DNA and RNA sequences. Detecting conserved motifs and patterns within sequences is crucial for understanding gene functions and regulations and for identifying functional and structural elements in the genome.

`SMT` is constructed using a sparse matrix that stores the k-mers and their respective nodes. The process of creating the `SMT` is performed by the `createSMT` algorithm, which inserts the k-mers into the matrix, ensuring time and space optimization.

The `ksearch` algorithm performs exact k-mer search in the `SMT`, checking whether the queried k-mer is present in the structure. The exact search is performed in constant time, making SMT an efficient tool for large-scale analyses.

The `KIUPACscan` is a specialized search function designed to identify and count patterns specified in IUPAC format within a `SMT` data structure. The IUPAC format is a standard way of representing nucleic acid sequences, making this algorithm particularly useful for bioinformatics and the study of genetic sequences. When an IUPAC pattern is provided to the function, it traverses the `SMT` to identify all instances of this pattern. The function then returns all the kmers that match the IUPAC pattern along with their counts, stored in a map where each kmer is mapped to its respective count. This provides a concise, high-level summary of all locations in the `SMT` where the pattern of interest occurs, as well as how frequently each associated kmer is found.

The `Kdive` is responsible for approximate search in the `SMT`, allowing for the discovery of k-mers with up to `d` uniformly distributed mutations across their bases. The approximate search is performed in linear time, making the analysis of variations within DNA and RNA sequences fast and accurate. This is particularly useful in discovering conserved motifs, in which the patterns are similar but not identical.

The `Hmap` was devised to swiftly extract a map containing all the kmers and their respective frequencies from the `SMT`. The efficiency and speed of `Hmap` are attributed to its direct execution on the `SMT` tree structure, which facilitates organized access and recovery of kmers and their counts. This approach leverages the hierarchical and organized nature of the `SMT`, allowing for efficient traversal of the tree to compile the kmer map. The synergy between the tree structure of the `SMT` and the efficient execution of `Hmap` results in a powerful tool that provides quick and precise extraction of the kmer map, thus facilitating subsequent genomic analyses.

The algorithm `KHmap` improves the capabilities of `Hmap`, allowing for the extraction of kmer maps for any value of `k` lesser or equal to `kmax`. This feature is particularly useful when the `SMT` has been constructed for a specific value of `k`, such as `k = 30`, for instance. In this case, `KHmap` can efficiently extract all corresponding maps for `k = 1, 2, 3, . . . , 30`, providing a flexibility that is a significant differential of the `SMT` in comparison to other related data structures. Although `KHmap` is slightly slower compared to `Hmap`, its ability to extract maps for a variety of values of `k` makes it a preferable choice whenever analysis for multiple values of `k` is required.

By combining these algorithms, the `SMT` offers an efficient and robust solution for genomic data analysis, contributing to a better understanding of gene functions and regulations and assisting in the identification of functional and structural elements in the genome.

## When to use SMT
`SMT` was built with the main objective of assisting in the analysis of biological motifs. However, it can be used in any situation in which it is necessary to count kmers or perform operations on kmers, such as knowing which are the most frequent or which are the most frequent considering a certain number of mutations.

## Getting Started
Follow the instructions below to be able to run SMT.

### Prerequisites and dependencies
Before installing the SMT package, make sure you meet the following prerequisites.

#### Operating System
- Linux

#### Programming Language
- C++17

#### Compilation Flags
- `-std=c++17`
- `-O3`
- `-march=native`
- `-fopenmp`
- `-DARMA_64BIT_WORD`
- `-DARMA_USE_HDF5`
- `-Wno-ignored-attributes`
- `-I/usr/include/hdf5/serial`

#### Linker Variables
- `-L/lib/x86_64-linux-gnu`
- `-L/usr/lib`

#### Libraries
To run this project, the following dynamic libraries are required:

- `libboost_filesystem.so.1.74.0`
- `libtbb.so.12`
- `libstdc++.so.6`
- `libgomp.so.1`
- `libgcc_s.so.1`
- `libc.so.6`
- `libm.so.6`

#### Linker Variables
- `-lboost_system`
- `-lboost_filesystem`
- `-lR`
- `-lblas`
- `-lz`
- `-ltbb`

#### Dependencies
To install the required dependencies, you can use the following command:

```bash
sudo apt-get install libboost-filesystem-dev libtbb-dev libstdc++6 libgomp1 libgcc1 libc6 libm6
```

## Quick Start

### Instalation
#### Step 1: Download the Binary Files

First, you need to download all the contents of the bin directory from this GitHub repository. You can do this easily with svn. First install subversion: ```sudo apt install subversion``` and then run the following command within the directory in which you want to install `SMT`: ```svn export https://github.com/jadermcg/smt/trunk/bin```.

#### Step 2: Place the Binary Files
After downloading, place the binary files in a directory of your choice on your computer. For example, you could place them in a folder called `smt/bin` under your home directory. If you created the biomapp_chip directory and downloaded the files there, run this command line to make files executable ```sudo chmod -Rf u+x bin```.

#### Step 3: Update the PATH Environment Variable
Lastly, you need to update your PATH environment variable to include the directory where you placed the binary files. You can do this using the `export` command in Linux. Open your terminal and run the following command:

```bash
export PATH=$PATH:/path/to/your/smt/bin
```
You can place this command inside your local user's .bashrc file so that you don't have to type it every time a command terminal is opened.

```
echo 'export PATH=$PATH:/path/to/your/smt/bin' >> ~/.bashrc
source ~/.bashrc
```

#### Usage
```
Use: smt -i <fasta> -k <size of kmer> -s <priori memory allocation>
```
#### Example
To understand how the program works, you can run `SMT` on the example dataset that is provided in the project root.

```
biomapp -i MA0003.4.fasta.dust -k 14 -s 256
```
This execution of `SMT` will process the dataset MA0003.4.fasta.dust using kmers of length 14 with 256Mb priori memory allocation. Executing this command will create a smt_data directory in the same location where the statement was executed. Inside smt_data, we have two files, SMT.db which is the database with kmers and their respective counts and meta.txt, which has some metadata, such as batch quantities and size of k. After executing the above command, other algorithms can be executed, such as kdive, hmap and khmap.

**_All commands below need to be executed after creating the SMT.db database:_**

##### Ksearch
Searches for a specific kmers on SMT and returns their frequency.

```
Use: ksearch -kmer <kmer>
```

##### Hmap
Creates a file inside `smt_data` called `hmap.txt` with all kmer counts.

```
Use: hmap
```

##### KHmap
Extracts from `SMT` maps with size `k` less than or equal to `kmax` (`k `value that was used when creating the SMT.db database).
```
Use: khmap -k <size of kmer> > out_map.txt
```

##### Kdive
Creates a directory in `smt_data` called `kdive_dir`. Inside it, there is a .txt file with the kmers and the respective counts for each of the kmers present in the `kmers.txt` file.

```
kdive -kmers <path to kmers> -d <number of mutations>
```
