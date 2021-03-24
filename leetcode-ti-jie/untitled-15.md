# 3. Longest Substring Without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

Example 1:

Input: s = "abcabcbb"

Output: 3 Explanation: The answer is "abc", with the length of 3.

Example 2:

Input: s = "bbbbb"

Output: 1 Explanation: The answer is "b", with the length of 1.

Example 3:

Input: s = "pwwkew"

Output: 3 Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

Example 4:

Input: s = ""

Output: 0

```text
class Solution {    public int lengthOfLongestSubstring(String s)  {        Set occ = new HashSet();        int n = s.length();        int rk = -1,ans = 0;        for (int i = 0;i < n;i++) {            if(i != 0) {                occ.remove(s.charAt(i-1));            }            while (rk+1                occ.add(s.charAt(rk+1));                rk++;            }            ans = Math.max(ans,rk-i+1);        }        return ans;    }}
```

滑動窗口法：

rk最右端,i最左端 rk+1不在之前的hashmap裏,則直接加入向右擴

若存在或者rk+1超過n了的話,執行if操作,最左端向右走,每次都記錄ans的最大值.這樣走到最後就可以得出答案,

​

