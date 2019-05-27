# Tries

https://www.geeksforgeeks.org/advantages-trie-data-structure/

## Implementation of Trie
```java
// my implementation from leet code
class TrieNode{
    char val;
    Map<Character, TrieNode> charMap = new HashMap<Character, TrieNode>();
    public TrieNode(char val){
        this.val = val;
    }
}

class Trie {
    TrieNode head;
    /** Initialize your data structure here. */
    public Trie() {
        head = new TrieNode('\0');
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        insertHelper(head, word, 0);
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        return helperSearch(word, true);
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        return helperSearch(prefix, false);
    }
    
    private boolean helperSearch(String word, boolean exact){
        TrieNode curr = head;
        for (int i = 0; i < word.length(); i++){
            if (curr.charMap.get(word.charAt(i)) == null) return false;
            else curr = curr.charMap.get(word.charAt(i));
        }
        if (!exact){
            return true;
        } else {
            return curr.charMap.get('*') != null;
        }
    }
    
    private void insertHelper(TrieNode head, String word, int index){
        if (index == word.length()) {
            head.charMap.put('*', new TrieNode('*'));
        } else {
            if (head.charMap.get(word.charAt(index)) == null){
                head.charMap.put(word.charAt(index), new TrieNode(word.charAt(index)));
            }
            insertHelper(head.charMap.get(word.charAt(index)), word, ++index);
        }
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

## Applications
### Advantages of Trie Data Structure
Tries is a tree that stores strings. Maximum number of children of a node is equal to size of alphabet. Trie supports search, insert and delete operations in O(L) time where L is length of key.

Hashing:- In hashing, we convert key to a small value and the value is used to index data. Hashing supports search, insert and delete operations in O(L) time on average.

Self Balancing BST : The time complexity of search, insert and delete operations in a self-balancing Binary Search Tree (BST) (like Red-Black Tree, AVL Tree, Splay Tree, etc) is O(L Log n) where n is total number words and L is length of word. The advantage of Self balancing BSTs is that they maintain order which makes operations like minimum, maximum, closest (floor or ceiling) and k-th largest faster. Please refer Advantages of BST over Hash Table for details.

### Why Trie? :-

With Trie, we can insert and find strings in O(L) time where L represent the length of a single word. This is obviously faster that BST. This is also faster than Hashing because of the ways it is implemented. We do not need to compute any hash function. No collision handling is required (like we do in open addressing and separate chaining)
Another advantage of Trie is, we can easily print all words in alphabetical order which is not easily possible with hashing.
We can efficiently do prefix search (or auto-complete) with Trie.
### Issues with Trie :-
The main disadvantage of tries is that they need lot of memory for storing the strings. For each node we have too many node pointers(equal to number of characters of the alphabet), If space is concern, then Ternary Search Tree can be preferred for dictionary implementations. In Ternary Search Tree, time complexity of search operation is O(h) where h is height of the tree. Ternary Search Trees also supports other operations supported by Trie like prefix search, alphabetical order printing and nearest neighbor search.

The final conclusion is regarding tries data structure is that they are faster but require huge memory for storing the strings.