# Letter Tile Possibilities
## Leetcode Problem No. 1079 [Problem Link](https://leetcode.com/problems/letter-tile-possibilities/)
### Problem:
You have n  tiles, where each tile has one letter tiles[i] printed on it.

Return the number of possible non-empty sequences of letters you can make using the letters printed on those tiles.

Example 1:

Input: tiles = "AAB"
Output: 8
Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
Example 2:

Input: tiles = "AAABBC"
Output: 188
Example 3:

Input: tiles = "V"
Output: 1
 

Constraints:

1 <= tiles.length <= 7
tiles consists of uppercase English letters.

### Solution:
```
class Solution {
public:
    void permutation(string str,unordered_set<string> &s,int i){
        if(i==str.length()){
            s.insert(str);
        }
        for(int j=i;j<str.length();j++){
            swap(str[i],str[j]);
            permutation(str,s,i+1);
            swap(str[i],str[j]);
        }
    }
    int numTilePossibilities(string tiles) {
        unordered_set<string> s;
        int len=tiles.size();
        int n=1<<len;
        int count=0;
        for(int i=1;i<n;i++){
            string curr="";
            for(int j=0;j<len;j++){
                if(i&(1<<j)){
                    curr+=tiles[j];
                }
                
            }
            if(s.find(curr)==s.end()){
                permutation(curr,s,0);
            }
        }
        return s.size();
    }
};
```
