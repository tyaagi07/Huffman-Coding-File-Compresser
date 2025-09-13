<h1 align='center'>Huffman Zipper</h1>
<h3 align='center'>A simple file compressor and decompressor based on Huffman Coding in C++.</h3>

Huffman coding is a compression technique that constructs a tree from a collection of weighted nodes.
At the start, every character is treated as a single-node tree, where the weight is the frequency of that character.
By repeatedly merging the two least-weighted trees, we gradually form one final tree that represents the optimal encoding scheme.

🔹 Steps of the Algorithm

Initialization – Create a forest where each tree consists of a single node holding a character and its frequency (weight). Characters with high frequency have higher weights, and rare characters have lower weights.

Merge Process – Select the two trees with the smallest weights, call them T1 and T2. A new parent node is created with weight = T1 + T2. T1 becomes the left child and T2 the right child.

Final Tree – Repeat until only one tree remains. This tree becomes the Huffman encoding tree, which guarantees minimal average code length.

🔹 Implementation Approach

The project has two components:

Compression program (Huffing) → Reads a regular file and produces a compressed version.

Decompression program (Un-Huffing) → Reconstructs the original file from the compressed one.

Both programs rely on shared code such as data structures, helper functions, and tree-building logic.

🔹 Core Data Structures

Two hash maps (unordered_map in C++)

One maps each character to its frequency (occurrences).

Another maps each character to its Huffman code.

A priority queue (min-heap)
Used to efficiently select the two lowest-weight nodes during tree construction.

🔹 File Header Handling

To decode correctly, the decompressor must know the tree or frequencies used during compression. Possible approaches include:

Storing the frequency of every character (or only non-zero ones along with the character).

Using predefined frequency tables (e.g., for English text).

Writing the Huffman tree itself at the beginning of the file (e.g., via pre-order traversal with special bits to mark leaf vs. internal nodes).

🔹 Challenges Faced

One issue arises from bit-level writing. Operating systems typically buffer I/O and enforce file sizes in multiples of bytes (8 bits). For example, if the compressed output is 61 bits, the system will pad 3 extra bits to make 64.

This means our decompression program must correctly handle padding bits.
We achieve this by checking whether the encoded bit string length is divisible by 8. The remainder tells us how many padding bits were added, so we can safely ignore them during decompression.
