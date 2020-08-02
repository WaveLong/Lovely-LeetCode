49. Group Anagrams

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, int>mp;
        vector<vector<string>>ans;
        for(int i = 0; i < strs.size(); ++i){
            string key = strs[i];
            sort(key.begin(), key.end());
            if(mp[key]){
                ans[mp[key] - 1].push_back(strs[i]);
            }else{
                mp[key] = ans.size() + 1;
                ans.push_back(vector<string>{strs[i]});
            }
        }
        return ans;
    }
};
```

