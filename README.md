# **File Compression Using Huffman's Algorithm**

# About

Huffman Algorithm is an efficient way for file Compression and Decompression.
This program exactly follows huffman algorithm. It reads frequent characters from input file and replace it with shorter binary codeword.
The original file can be produced again without loosing any bit.

# Usage

Compression:

```
	./encode <file to compress>
```

Output file named <inputfile>.spd will be produced.
Decompression:

```
	./decode <file to uncompress>
```

# File Structure

<table>
<tr> <td colspan="2">  N= total number of unique characters(1 byte)              </td> </tr>
<tr> <td> Character[1 byte]   </td><td>  Binary codeword String Form[MAX bytes]  </td> </tr>
<tr> <td> Character[1 byte]   </td><td>  Binary codeword String Form[MAX bytes]  </td> </tr>
<tr> <td colspan="2">              N times                                       </td> </tr>
<tr> <td> p (1 byte)          </td><td> p times 0's (p bits)                     </td> </tr>
<tr> <td colspan="2">  DATA                                                      </td> </tr>
</table>

p = Padding done to ensure file fits in whole number of bytes. eg, file of 4 bytes + 3 bits must ne padded by 5 bits to make it 5 bytes.

## Example

Text: aabcbaab

| Content                             | Comment                               |
| ----------------------------------- | ------------------------------------- |
| 3                                   | N=3 (a,b,c)                           |
| a "1"                               | character and corresponding code "1"  |
| b "01"                              | character and corresponding code "01" |
| c "00"                              | character and corresponding code "00" |
| 4                                   | Padding count                         |
| [0000]                              | Padding 4 zeroes                      |
| [1] [1] [01] [00] [01] [1] [1] [01] | Actual data, code in place of char    |

# Algorithm

0. **(Pass 1)** Read input file
1. Create sorted linked list of characters from file, as per character frequency

   ```
   for eah character ch from file

   if( ch available in linked list at node p) then
   {
   	p.freq++;
   	sort Linked list as per node's freq;
   }
   else
   	add new node at beginning of linked list with frequency=1;
   ```

2. Construct huffman tree from linked list 0. Create new node q, join two least freq nodes to its left and right 0. Insert created node q into ascending list 0. Repeat i & ii till only one nodes remains, i.e, ROOT of h-tree 0. Traverse tree in preorder mark each node with its codeword. simultaneously Recreate linked list of leaf nodes.
3. Write Mapping Table(character to codeword) to output file.
4. **(Pass 2)** Read input file.
5. Write codeword in place of each character in input file to output file
   for each character ch from input file
   write corresponding codeword into o/p file (lookup in mapping table OR linked list)
6. End

# Development

To do:

- Binary files, like jpeg,mp3 support
- Run scan to group repeating bit patterns, not bit.
- Unicode support
- Move entire codebase to python, use neural network to compress files.
