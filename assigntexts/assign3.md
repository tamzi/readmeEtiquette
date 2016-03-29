I. File list
------------
AVLTNode.cc		AVL tree node (AVLTNode) implementation
AVLTNode.h		AVLTNode header
AVLTree.cc		AVL tree (AVLTree) implementation
AVLTree.h		AVLTree header
BinarySearchTree.cc	Binary search tree (BinarySearchTree) implementation
BinarySearchTree.h	BinarySearchTree header
BSTNode.cc		Binary search tree node (BSTNode) implementation
BSTNode.h		BSTNode header
main.cc			driver for word-count
Makefile		Makefile to build word-count
MaxHeap.cc		Specialized max binary heap (MaxHeap) implementation
MaxHeap.h		MaxHeap header
README			This file
SplayTree.cc		Splay tree (SplayTree) implementation
SplayTree.h		SplayTree header
TemplateInst.cc		Instantiation file for all templated classes
heapsort.ps             Plot file for heapsort w/ splay tree on 10 files
quicksort.ps            Plot file for quicksort w/ splay tree on 10 files
selectionsort.ps        Plot file for selection sort w/ splay tree on 10 files


Program can be built using default make arguments.



II. Design
----------
A. Program design

1. Style
Code given by CSE326 staff was treated as though it was written by a team
member.  Naming conventions of pre-existing code was changed to match the
team's preferred style for member functions.

2. Collision handling
It seemed apparent that because we were generalizing through templates, to have
the result of doing an operation on some key that already existed be hardcoded
was not in good form.  This is where the collision policy idea came to bear.
The general principal is that the end-programmer using a tree should be able to
specify what happens as a result of a collision by supplying a function to
handle this event.  In case the end-programmer does not know about function
pointers, or has no desire to specialize the trees by supplying a collision
function, a default must be set up.  This directly translates to the
unparameterized constructor (default), the parameterized constructor (with
collision function) and the setCollisionPolicy function (in case they need to
change).

3. bool <function>(param& , param&) signatures
We wanted to have a way to notify the user of invalid find operations.  Since
the code is templatized we dont know what type to return for the function.  Thus
the bool return.  Essentially, if the operation is successful, return true and
modify the appropriate parameter that was passed in by reference.  If the
operation fails, return false, and leave the parameter alone.  With this design
decision made, other similar functions needed to have similar feels to maintain
a consistant API.


B. AVL Tree

1. Insertion
An interative insert function was written to give better performance because
recursive functions has to allocate/deallocate multiple stack frames.

2. AVLTNode
Because an AVL tree is a self-balancing tree, the node structure needs to be
extended to handle height information.


C. Splay Tree

1. Iteration vs. Recursion
Iteration was chosen specifically for code reuse purposes. The general algorithm
for any splay tree operation was to perform the operation then splay at that
particular node. Using the provided functions from the binary search tree code
allowed finding a particular node easy. Then once found, it was a matter of
simply splaying it to the root (while its not the root, splay it). The specific
algorithm for inserting was taken directly from the BST code, with only small
modifications for splaying and personal preferences on handling returns (try to
have return keyword in only one place).  

2. Small functions
They are easier to test, easier to code, easier to read,and definitely easier to
understand. The general concept is to minimize the syntax baggage for public
interface functions, letting them act as drivers, and have protected functions
do the gruntwork.

3. zig, zigZig, zigZag
Named after the operations that we discussed in class, these are the driver
functions for rotation.  Their names attempt to describe the general pattern
(although each describes two different symmetrical patterns) of a
node-parent-grandparent relationship.  In each function, there are calls to the
appropriate hanging function to simulate the rotation (see 5 for more
information).  Because of the binary ordering properties of a splay tree, each
function could make a set of assumptions on the data as to how to rotate, or
hang parent nodes.

4. hangPLeft, hangPRight 
The heart of rotation, these functions perform the basic operation of "hanging"
a parent (P) off of its child in a function name specified direction.  They
handle all of the pointer manipulation that maintains proper tree structure.
Although synonymous with rotation to some degree, it was felt that "hanging" and
direction gave a more complete and accurate description of what the function was
doing compared to "rotating".  Specifically, a rotation is nothing more than
hanging a parent off of its child, and a double rotation is nothing more than a
strictly ordered coupling of these hang operations.


D. Binary Heap (MaxHeap)

1. Specialization
Specializations were made to the binary heap.  This includes the omission of an
insert() function, no generic node type for the array, and making it a max heap.
Max heap was the most logical choice for this assignment because this assignment
dealt with word frequency.


2. Implementation
The MaxHeap was implemented using parallel arrays, one each for words and
frequency.  buildHeap() was implemented using Floyd's algorithm, which runs in
O(n).


3. heapSort()
This was not implemented as a member function of the MaxHeap class.  The basic
algorithm for this function is to print the maximum value in the heap and then
delete the maximum value.  The deletion will also call percolateDown() on the
new root.  The printMax() method used in heapSort() is the main bottleneck of
this algorithm due to the calls to the system I/O.



III. Analysis
-------------
The text of both authors, Bacon and Shakespeare, show a predominance of the
words "the," "of," and "and."  In Bacon's "The Essays" and "The New Atlantis,"
these common words are occurring approximately 12.4% and 14.3% of the time,
respectively.  In Shakespeare's "Hamlet" and "All's Well That Ends Well," these
words occur approximately 6.86% and 6.56%, respectively.  Based on this
evidence, we conclude that Bacon did not write Shakespeare's works.

Take that, you conspiracy theorists.



IV. Expected Bottlenecks
------------------------
A. Binary Search Tree

1. insert()/findNode()
It was hard to separate these two functions because insert() relies on
findNode() as a part of its algorithm.  This takes the longest in the BST
because it has no balancing properties.  In the case of this sorted list, it is
essentially a doubly-linked list with O(n) running time.


2. getDataAsArray()/recursiveCopy()
Stack frame allocation/deallocation from recursiveCopy() kills the performance
of these functions.


B. AVL Tree


1. insert()/findNode()
This needs to call findNode() from the BinarySearchTree class, which takes
O(log n).


C. Splay Tree


1. insert()
Similar to the AVL Tree, this needs to call findNode() from the BinarySearchTree
class, which takes O(log n).

2. splay()
This has to be called every time.  Although this is a constant time operation
for sorted input, the total running time will be linearly proportional to the
amount of data.


3. hangPRight()
This again is called every time.  It is interesting to note that this was called
twice as many times as insert(), though only one rotation is done per insert.



V. Real Bottlenecks
-------------------
A. Data weirdness

1. findNode()/std::min()
When looking at the data for the BinarySearchTree, findNode() was found to
take approximately 85% of the running time with approximately 45,000 calls.
However, std::min() makes approximately 231,000,000,000 calls but only takes
15.5% of the running time.  We believe the data is skewed/inaccurate because of
these findings.


B. Binary Search Tree

1. insert()/findNode()
As expected, these two functions took most of the processing time.

2. getDataAsArray()/recursiveCopy()
Again, as expected, these algorithms took a long time to run, although only
one call was made to getDataAsArray().


C. AVL Tree

1. insert()
This took the longest of the AVLTree functions at approximately 6.14%.


D. Splay Tree

1. insert()
Total processing time was approximately 2.11%.  


2. splay()
Total processing time was also approximately 2.11%.


3. hangPRight()
This also took approximately 2.11%.  However, it is interesting to note that
twice as many hangPRight() calls were made compared to splay().



VI. Sorting Algorithm Analysis
------------------------------

1. HeapSort - Heapsort normally runs in N log N for best, worst and average case
   It is thus reasonably efficient for binary comparisons. It should on average run
   in parallel with quicksort.

2. Selection Sort- Selection Sort is supposed to run in N^2 time for worst and best
   case scenario, and thus should be the worst of the three algorithms, except for
   extremely aberrant input.

3. QuickSort- Quicksort should run in N log N for best and average case scenarios.
   Again, it is reasonably efficient on binary comparisons and should be running
   equally well as heapsort.


In reality, heapsort is clearly the most efficient on our particular data set. We
speculate that the reason it outperforms quicksort for all the inputs is that
quicksort is not running at average time - our input is a poor represenatation of
average input for quicksort. Specifically, the input is very dense, so that many
of the different items have the same value, and thus a lot of swapping must occur,
slowing a normally fast algorithm down. It still is not obviously enough to force
quicksort to run at *worst* case time, as it still better than selection sort.
Essentially, heapsort is less affected by our semi-aberrant data than quicksort,
and selection sort is pretty bad for large data sets to begin with.

(See plots for reference)


