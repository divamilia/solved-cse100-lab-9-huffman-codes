Download Link: https://assignmentchef.com/product/solved-cse100-lab-9-huffman-codes
<br>
<h1>Huffman Codes</h1>

<strong>Description   </strong>Suppose that we have to store a sequence of symbols (a file) efficiently, namely we want to minimize the amount of memory needed. For the sake of simplicity we assume that the symbols are restricted to the first 6 letters of the alphabet. For example, let us assume that the frequency of different symbols that you have to store are the following: symbol            frequency

A            1000 B  150

<ul>

 <li>200</li>

 <li>800</li>

 <li>300</li>

 <li>50</li>

</ul>

Total         2500

As we have to store 6 different symbols, the obvious way is to encode each of them in 3 bits, as with 3 bits it is possible to encode 2<sup>3 </sup>different symbols. With this encoding, we need 2500×3 = 7500 bits to store the above symbols. A different way to address the problem is the following. Instead of assigning to each symbol a code with the same length (i.e., number of bits), we assign shorter codes to symbols that are more frequent, and longer codes to symbols that are less frequent. One possible encoding according to this sequence is the following symbol    encoding

<ul>

 <li>0</li>

 <li>10101</li>

 <li>1011</li>

 <li>11</li>

 <li>100</li>

 <li>10100</li>

</ul>

According to this encoding the number of required bits is:

1000 × 1 + 150 × 5 + 200 × 4 + 800 × 2 + 300 × 3 + 50 × 5 = 5300<em>.</em>

This idea is at the basis of the programs used to compress files. First they analyze the input, then they choose the codes, and then they recode the input according to the determined codes.

While this idea brings benefits in terms of the space requirements, using variable length codes presents some problems. Once we have coded a file according to a variable length code, we must also be able to decode it in the original format (i.e., once we have compressed the file, we want to able to decompress it). The encoding works only if the codes assigned to different characters are such that no code is a prefix of any other code. If this property does not hold, there is a problem of ambiguity when trying to decompress the sequence.

You can prove that in the depicted example no code is a prefix of any other code. For example: no code starts with 0 except from the code of <em>A</em>. So while decompressing the file, if we find a

symbol whose code starts with 0, we know it’s <em>A</em>. If we find a character whose code starts with 11, we know it’s <em>D</em>. It can’t be any other symbol, as no code starts with 11 other than <em>D</em>’s code. And so on. How do we assign codes? This is done through a greedy algorithm. We assign the shortest code to the most frequent character, the second longest one to the second most frequent character, and so on. The figure below illustrates the first few stages of the algorithm.

Given <em>N </em>characters with their respective frequencies, the algorithm initially builds <em>N </em>trees, each one consisting just of a single node (step 1, in the figure). Then, iteratively, it joins together the trees whose roots have the lowest frequencies (steps 2, 3, etc. in the figure). <em>The tree with the lowest root frequency becomes the left child and the tree with the second-lowest root frequency becomes the right child</em>. Left children are associated with the bit 0, right children with the bit 1. Internal nodes (i.e., root nodes created) can be thought of as dummy nodes storing a fictitious character (which does not appear in our sequence). This procedure is iterated until there is just one tree. At this point, in order to know the code associated with one symbol you simply need to concatenate the 0s and 1s you encounter while moving from the root down to the symbol.

Note that the greedy strategy is applied in the reverse way. Symbols with low frequencies end up down in the tree (i.e., they are associated with long codes), while nodes with high frequencies are near the root (i.e., they are assigned short codes).

<strong>Questions and input structure </strong>The input consists of 6 integers, one per each line. Each integer represents the frequency of characters, A, B, C, D, E, and F, in this order. The test cases have been built so that while building trees it never happens that the same frequency appears twice. Then, the decision about which tree goes to the left and which one goes to the right is always straightforward, and the final tree should be unique.

<strong>Examples of input and output</strong>

<em>Input</em>

15

11

5

1

2

4 <em>Output</em>

A:0

B:10

C:110

D:11100

E:11101

F:1111

See the lab guidelines for submission/grading, etc., which can be found in Files/Labs.