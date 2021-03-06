### BoardFolding Problem
Adapted from Topcoder SRM 639 (BoardFolding) D1 500 point problem\
\
Little Petya likes puzzles a lot. Recently he has received one as a gift from his mother. The puzzle has the form of a rectangular sheet of paper that is divided into N rows by M columns of unit square cells. Rows are numbered 0 through N-1 from top to bottom, and columns 0 through M-1 from left to right. Each cell is colored either black or white. You are given a description of the paper, the exact format is specified at the end of this problem statement.\
\
The goal of the puzzle is to fold the paper. This has to be done in a sequence of turns. In each turn, Petya has to fold the paper according to the rules below. He can end the process after any number of turns (including zero), even if there are still valid ways to fold the paper.\
\
In each turn, Petya must follow these steps: To start folding, he must choose a line that is parallel to one of the sides of the paper and passes between two rows/columns of cells. He can then take the smaller part of the paper and fold it on top of the larger part. (If the line divides the current paper in half, he can fold either half on top of the other.) There is one additional restriction: Petya may only perform the fold if all cells of the part that is being folded land on equally-colored cells of the part that remains in place.\
\
For example, consider the following paper (with 0 and 1 representing white and black):\
\
10010101\
11110100\
00000000\
01101110

Here, Petya could choose the vertical line that goes between the two leftmost columns and the rest of the paper. Note that this is a valid choice: as he makes the fold, the cells from the leftmost two columns will all match their counterparts in the right part of the paper. This is how the paper looks like after the fold (with periods representing empty spaces):\

..010101\
..110100\
..000000\
..101110

Clearly, even after multiple folds the paper will always look like a subrectangle of the original paper. Two states of the game are considered the same if that rectangle has the same dimensions and the same offset with respect to the original top left corner of the paper. (Note that folding order does not matter. Two different sequences of folding may produce the same final state.)

You are given the ints N and M. You are also given a description of the original state of the paper in a compressed form, as a vector <string> compressedPaper. Compute and return the number of possible final states of the game.

The vector <string> compressedPaper will contain N elements with ceil(M/6) characters each. Each character (except possibly the last one) encodes six cells of the paper. The actual paper can be obtained from compressedPaper using the following pseudocode:

```
for i in 0..N-1:
    for j in 0..M-1:
        paper[i][j] = (tonumber(compressedPaper[i][j / 6]) >> (j modulo 6)) modulo 2
```
 
In the above pseudocode, "/" represents integer division (rounding down), ">>" is a bit shift to the right, and tonumber(x) maps the character x to a number between 0 and 63 as follows: the characters '0'-'9' map to integers 0-9, 'a'-'z' map to 10-35, 'A'-'Z' map to 36-61, '#' maps to 62, and '@' maps to 63.

If paper[i][j] = 0, then the cell (i,j) is white, otherwise it is black.

### Definition
**Class:** BoardFolding\
**Method:** howMany\
**Parameters:** int, int, vector <string>\
**Returns:** long long \
**Method signature:** long long howMany(int N, int M, vector <string> compressedPaper)

#### Constraints
- N and M will be between 1 and 3000, inclusive.
- compressedPaper will contain N elements.
- Each element of compressedPaper will contain ceil(M / 6) elements.
- compressedPaper will contain only characters '0'-'9', 'a'-'z', 'A'-'Z', '#' and '@'.

### Examples
\
0)\
2\
2\
{"1", "3"}\
\
Returns: 1\
\
The paper looks as follows:\
\
10\
11\
\
There is no valid way to fold this paper, so there is just one possible outcome.\
\
1)\
2\
7\
{"@@", "@@"}\
\
Returns: 84\
\
In this case the paper looks like this:\
\
1111111\
1111111\
\
We can fold it into any of the 84 possible subrectangles of the original rectangle.\
\
2)\
4\
4\
{"6", "9", "9", "6"}\
\
Returns: 9\
\
Here the paper is:\
\
0110\
1001\
1001\
0110\
\
3)\
6\
1\
{"0", "2", "6", "@", "4", "A"}\
\
Returns: 6\
\
Here the paper is:\
\
0\
0\
0\
1\
0\
0\
\
4)\
3\
3\
{"0", "2", "0"}\
\
Returns: 1\
\
In this case the paper looks like:\
\
000\
010\
000

### My solution
My solution is in [BoardFolding.cpp](https://github.com/EvanEzell/Topcoder/blob/master/BoardFolding/BoardFolding.cpp). It is O(n^2) time complexity.
