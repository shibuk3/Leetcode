# Binary Watch
## Leetcode Problem No. 401 [Problem Link](https://leetcode.com/problems/binary-watch/)
### Problem:
A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59). Each LED represents a zero or one, with the least significant bit on the right.

For example, the below binary watch reads "4:51".


Given an integer turnedOn which represents the number of LEDs that are currently on, return all possible times the watch could represent. You may return the answer in any order.

The hour must not contain a leading zero.

For example, "01:00" is not valid. It should be "1:00".
The minute must be consist of two digits and may contain a leading zero.

For example, "10:2" is not valid. It should be "10:02".
 

Example 1:

Input: turnedOn = 1
Output: ["0:01","0:02","0:04","0:08","0:16","0:32","1:00","2:00","4:00","8:00"]
Example 2:

Input: turnedOn = 9
Output: []
 

Constraints:

0 <= turnedOn <= 10

### Solution:
```
class Solution {
public:
    void help(vector<int> &h,int turnedOn,vector<string> &v,int i,int hr,int min){
        if(hr>11 || min>59) return;
        if(turnedOn==0){
            string curr=to_string(hr)+":";
            string t=to_string(min);
            if(t.length()<2) t='0'+t;
            curr+=t;
            v.push_back(curr);
            return;
        }
        if(i==10) return;
        if(i<4){
            help(h,turnedOn-1,v,i+1,hr+h[i],min);
            help(h,turnedOn,v,i+1,hr,min);
        }
        else{
            help(h,turnedOn-1,v,i+1,hr,min+h[i]);
            help(h,turnedOn,v,i+1,hr,min);
        }
        
    }
    vector<string> readBinaryWatch(int turnedOn) {
        vector<int> h={8,4,2,1,32,16,8,4,2,1};
        vector<string> v;
        help(h,turnedOn,v,0,0,0);
        return v;
    }
};
```
