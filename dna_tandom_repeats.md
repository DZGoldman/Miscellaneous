# Finding Tandem Repeats

### My Approach (prior to doing research)

#### General Idea
 Create a hash map of all 5-character substrings. The attributes will include the number of times each substring appears, the indices of each appearance of the substring, and the count of each of the letters that follow the string (similar to a  markov chain). From this, the tandem repeats of the 5-character substrings can be deduced. Then, by comparing the final 4 characters of each substring to each next possible character, the 6-character substrings can be deduced, and their tandem repeats can be deduced in the same fasion. This process will repeat until no n-character substrings with a sufficiently high count remain.

#### Algorithm

1. Input a DNA string of length n

- Split string into array of length n - 4, where each element is a substring of 5 characters starting at each element of the original string. i.e, "ACCCBEET" becomes

  ["ACCCB", "CCCBE", "CCBEE", "CBEET"]

  We'll call these elements "5-strings."

- Loop through each substring and create the following nested hash map:

  ```rb
  {
    Substring: {
        count: integer,
	    indices: array of integers,
	    A: integer,
        C: integer,
        T: integer,
        G: integer,
        }
  }
  ```

  In this hash, "count" is the number of times the 5-string appears, "indices" is an array of the index of each appearance, and "A", "C", "T", and "G" are the counts of the appearances of each letter following the substring.
- Create empty array: solution =[ ]  
- Iterate through each key in the main hash map:
 -  If the count is <= 4, remove it
 - Otherwise, iterate through the indices to see if there are 4 or more consecutive 5-strings with a common difference of the key (in this case 5)
    - If there are, store the starting index, count, and size in the solution array (store as a hash)
    - Check if the integer value for the **letterkeys** "A", "G", "T", or "C" keys are >=5
      - If so are, generate a new 6-string, where
        newSixString = oldFiveString++ oldFiveString[l**etterkey**]
      - Let the subtring lastFiveCharacters be the last five characters of newSixString
      - By retrieving index and integer count data from the lastFiveCharacters, pass on appropriate letter-counts and indices to newSixString
- Repeat step 5 step with 6-strings, and repeat until no keys have a  count greater than 4

#### Complexity
This algorithm runs in O(n^2) time. Steps 2 and 3 (creating the hash map) clearly take O(n) time. Note that the hash map that is created has, at most, 4^5 keys; thus, the iteration through the keys takes O(c) time. With each step of this iteration, however, each string's indices must be iterated through, which takes O(n) time. Since this must be repeated for each length of substring, which obviously increases linearly with the size of the inputed string, this gives a second linear factor of O(n), leading to an overall complexity of O(n^2). I would add, however, that since this second term is dependent upon the size of the maximum tandem repeat, the worst case scenario implied by O(n^2) is highly unlikely.

### Optimal Approach (via reserach)


#### Preliminary Definitions/ Terms
**Suffix Tree**

A suffix of a string is a substring that contains the final character of the string.

To construct a suffix tree, in graph-theoretical terms, each suffix is represented as a path from a root element to its final element. Nodes represent different possibilities for an element's subsequent elements; for example, in the simple string "TCTG", the "T" node would split into two branches; a "G" branch and a "CTG" branch.


A result of successfully building a suffix tree is that each leaf uniquely represents one of the n suffixes (this suffix can be generated from the leaf by simply starting at the leaf and working one's way up back to the root.)

##### Branching vs Non-branching Repeats:
A non-branching tandem repeat is one in which the character following the repeat is equal to the repeat's first character. For example:

AABB AABB A

is a non branching repeat of AABB, since the repeat is followed by A, the initial character. Repeats in which this does not hold are called branching repeats.

It should be noted that any non-branching occurrence of a repeat starting at index i can be obtained by 'left- rotating' (moving the final digit to the front) a tandem repeat starting at index i+1. In the above example:


1) AABB AABB (non-branching occurrence of tandem repeat)

2) ABBA ABBA (tandem repeat starting at index i+1)

left rotate 2, and you get 1.

It follows from this that if all branching repeats in our string could be obtained, the non-branching repeats could then be obtained by performing a series of left rotations.

#### Theorem
The following follows directly from the properties of a suffix tree and the above definitions: claiming that there is a branching tandem repeat at index i of length L is equivalent to claiming that i and j (where j is the final index of the repeat) both exists in the same leaf-list of some node in our suffix tree with depth= L/2 but not in any leaf list of a node with suffix >L/2.

 To put this another way: if the string [i..j] is a tandem repeat of lenth L, then one will be able to find a node that has the string as a direct child by starting at the root and traveling down L/2 steps; however, none of this node's ancestors will have the string as a direct child.

#### Algorithm

Our definitions and theorems  contain all of the basic building blocks of the algorithm.

The first step in the algorithm is to construct a suffix tree out of the DNA-string of length-n. The structure that can be used is a hash map where each key-value pair is a suffix and its index in the full DNA string; the node-structure is recreated with recursive calls into the hash map itself whenever a node is reached.

Next, iterate through each of the characters in the DNA-string; these are all of our potential starting points for a tandem repeat.
For each character, obtain the substring of length L and search for all nodes with depth L/2 in the suffix tree. If the substring appears, its appearance represents an instance of a branching repeat. Using the left-rotation process described above, all non-branching repeats can be obtained by rotating these branching repeats.




## My Approach Vs. Optimal Approach
Obviously the two approaches are completely different, but the key mistake that I was making in my thinking was using a Markov-chain-esque structure. Markov chains, by there very nature, are limited, in that none of the characters retain information about the characters prior to them. The suffix tree structure elegantly solves this; it is, essentially, traversable in both directions, making it much more informationally efficient.
