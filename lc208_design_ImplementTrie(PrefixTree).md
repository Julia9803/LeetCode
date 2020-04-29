### 208. Implement Trie (Prefix Tree)

Implement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

- You may assume that all inputs are consist of lowercase letters `a-z`.
- All inputs are guaranteed to be non-empty strings.

#### Solution:

```java
class Trie {
    
    class TrieNode {
        public TrieNode[] child;
        public boolean isword;
        
        public TrieNode() {
            child = new TrieNode[26];
            isword = false;
        }
    }
    
    private TrieNode root;

    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        for(int i = 0;i < word.length();i++) {
            char c = word.charAt(i);
            if(node.child[c-'a'] == null) {
                node.child[c-'a'] = new TrieNode();
            }
            node = node.child[c-'a'];
        }
        node.isword = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode node = root;
        for(int i = 0;i < word.length();i++) {
            char c = word.charAt(i);
            if(node.child[c-'a'] != null) {
                node = node.child[c-'a'];
            } else
                return false;
        }
        return node.isword;
        // TrieNode node = find(word);
        // return node != null && node.isword;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for(int i = 0;i < prefix.length();i++) {
            char c = prefix.charAt(i);
            if(node.child[c-'a'] != null) {
                node = node.child[c-'a'];
            } else return false;
        }
        return true;
        // TrieNode node = find(prefix);
        // return node != null;
    }
    
    // public TrieNode find(String word) {
    //     TrieNode node = root;
    //     for(int i = 0;i < word.length();i++) {
    //         char c = word.charAt(i);
    //         if(node.child[c-'a'] != null) {
    //             node = node.child[c-'a'];
    //         } else
    //             return null;
    //     }
    //     return node;
    // }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

##### Date 2020.4.29