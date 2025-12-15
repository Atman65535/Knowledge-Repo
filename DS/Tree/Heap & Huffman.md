
# Heap

A heap is a specialized tree-based data structure that satisfies **Heap Property**. Most efficient way to implement a **Priority Queue**/

### Key Properties of a Binary Heap
1. Node index $i$:
	- left child at $2i+1$, right at $2i+2$, parent at $(i-1) //2$. (zero based)
	- left child at $2i$, right at $2i+1$, parent at $i//2$.(one based)
2. Heap Property: Root >= left, Root >= right. Vice versa. 

### Operation
1. Insert $O(\log n)$: add to last one, and maintian father nodes iterately.
2. Extract $O(\log n)$: extract, exchange with last one, maintain heap from head to root iterately.
3. Build from array $O(n)$: from node index $n//2$ (one based) or $(n-1)//2$ (zero based), maintain heap.

# Huffman Tree

### Variable-Length Prefix Codes
Prefix codes is align with binomial tree.
- the last two frequence node must appears at the farest node of tree.
- the prefix code tree have and only have two leaf node at last layer, other layer only have 1.
Then we have a iterative structure: Extract two minimum, combine them.

Assign 0 to left, 1 to right. OK.