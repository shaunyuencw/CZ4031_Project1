
# CE4031-CZ4031: Database Management System Project

## Introduction

In this project, we tackle a foundational element of database management systems, emphasizing the essential components of storage and indexing. Efficiently storing and retrieving information is paramount for the performance and functionality of any database system. Our indexing component leverages a B+ tree structure, housed in main memory, to bolster efficient data operations. Throughout this documentation, the terms "records" and "tuples" are utilized interchangeably.

## Data

The data set used in the experiments represents statistics of NBA teams from 2003 to 2022. The data set can be downloaded from [this link](https://www.dropbox.com/scl/fi/s4wgb8uspaq1bog6tbyby/games.txt?rlkey=gmc0i28bs53mmxovcewpc4mlx&dl=0).

## Installation & Setup

### Step 1: Clone the Repository
Open your terminal and execute the following command to clone the project:
`git clone https://github.com/shaunyuencw/CZ4031_Project1.git` 

### Step 2: Navigate to the Project Directory

Once the repository is cloned, navigate to the project directory:
`cd CZ4031_Project1` 

### Step 3: Prepare the Data File

Ensure you have the `games.txt` data file. If not, download it from the provided link. After downloading, place it in the root directory of the project or in a directory of your choice.

### Step 4: Run the Application

If you're using an IDE like IntelliJ IDEA or Eclipse:

-   Import the project.
-   Locate and execute `Main.java`.
-   Upon prompt, input the path to `games.txt`.

Alternatively, if you're compiling and running through the terminal:
`javac Main.java`
`java Main` 

Then, follow the on-screen instructions and provide the path to `games.txt` when prompted.

## Storage Component

### Implementation Overview

Our first step involved defining the size of each attribute within a record. Having scrutinized the data, we outlined data types that enabled us to attain an optimal calculation size within our set block size of 400 bytes. This block is capable of hosting 20 records, with each record being 20 bytes. The record's attributes are specified below:

| Attribute     | DataType (Size) |
|---------------|-----------------|
| gameDateEst   | Int (4 bytes)   |
| teamIdHome    | Int (4 bytes)   |
| ptsHome       | Byte (1 byte)   |
| fgPctHome     | Float (4 bytes) |
| fg3PctHome    | Float (4 bytes) |
| astHome       | Byte (1 byte)   |
| rebHome       | Byte (1 byte)   |
| homeTeamWins  | Byte (1 byte)   |
	_Total size: 20 bytes_

Our storage capacity was determined based on the number of rows in the provided dataset. We concluded that a 100MB storage suffices, granting us 250,000 blocks, thereby enabling storage for up to 5,000,000 records. This is evident from the equation:

Number of Records=250,000 blocks×20 records per block=5,000,000 recordsNumber of Records=250,000 blocks×20 records per block=5,000,000 records

### Core Classes for the Storage Component

1.  **Record.java**: A representation of a row in a database, mirroring the structure found in "games.txt". Each instance corresponds to a singular record, encompassing all related data.
    
2.  **Block.java**: A container to manage records within the fixed-sized block of 400B. It oversees the number of records it holds, monitors available space, and offers methods for record operations.
    
3.  **Address.java**: Vital for pinpointing specific records, encapsulating block location and the offset within the block.
    
4.  **Database.java**: Represents the entire storage component, managing an array of blocks and maintaining data organization.
    

## Index Component

The indexing component is anchored by the B+ tree structure.

### Core Classes for the Index Component

1.  **Node.java**: Represents individual nodes, with each node possessing an array of keys which the database is indexed on.
    
2.  **InternalNode.java**: Inherits from `Node.java` and maintains an array of Nodes representing child nodes.
    
    _Visual Representation_: `[Pointer | Key | Pointer | ...]`
    
3.  **LeafNode.java**: Inherits from `Node.java`, but rather than child nodes, it tracks an array of `<Key, Array<Address>>` pairs, in addition to its sibling nodes. Each key in a LeafNode corresponds to an array of addresses.
    
4.  **BPlusTree.java**: Represents the overall B+ Tree structure. This class also orchestrates the operations for experiments 2 through 5.
    
5.  **BPTHelper.java**: A supplementary class aiding in counting node-reads for experiments 3 and 4.
    

### Key Operations

-   **Insertion (insertKeyAddrPair)**: We can perform bulk insertions, but we've opted for sequential insertion of key-value pairs for this project. This choice might lead to the underutilization of LeafNodes.
    
-   **Deletion**: Encompasses borrowing of keys and merging of leaves. Various methods are invoked when deleting a single key.

## Group Members & Contributions

### Darryl (@ddaarrrryyll)
- **Primary Role**: Lead Developer
- **Contributions**: 
  - Designed the core architecture of the database management system.
  - Led the team in various coding sessions.
  - Collaborated with Shaun on optimizing the indexing component.
  - Code review and testing.

### Shaun Yuen (@shaunyuencw)
- **Primary Role**: Indexing Specialist
- **Contributions**: 
  - Oversaw the implementation of the B+ tree structure.
  - Worked with Darryl to optimize data retrieval times.
  - Developed the algorithms for efficient data insertion and deletion.
  - Contributed to the documentation on the indexing component.

### Jie Chung Ong (@burntpie)
- **Primary Role**: Storage Architect
- **Contributions**:
  - Designed and implemented the storage component.
  - Developed the `Block.java` and `Address.java` classes.
  - Managed data storage and retrieval.
  - Assisted Abhishekh in data analysis for experiments.

### Abhishekh Pandey (@AbhishekhPandeyVats)
- **Primary Role**: Data Analyst & Documenter
- **Contributions**: 
  - Handled the analysis of data for experiments.
  - Worked with Jie Chung on integrating the storage component with the B+ tree.
  - Responsible for writing and compiling the group's report.
