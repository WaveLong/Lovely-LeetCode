93. Restore IP Addresses

Medium

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

**Example:**

```
Input: "25525511135"
Output: ["255.255.11.135", "255.255.111.35"]
```

**Solution**

动态规划。类似于斐波那契数列

```c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        vector<string>tmp;
        vector<string>ans;
        dfs(s, tmp, ans, 0);
        return ans;
    }
    void dfs(string &s, vector<string>&tmp, vector<string>&ans, int index){
        if(index >= s.size() && tmp.size() == 4){
            string str = tmp[0];
            for(int i = 1; i < tmp.size(); ++i)str = str + "." + tmp[i];
            ans.push_back(str);
            return;
        }
        if(index >= s.size())return;
        if(tmp.size() >= 4)return;
        tmp.push_back(s.substr(index, 1));
        dfs(s, tmp, ans, index + 1);
        tmp.pop_back();
        if(index + 1 < s.size() && s.substr(index, 2) <= "99" && s.substr(index, 2) >= "10"){
            tmp.push_back(s.substr(index, 2));
            dfs(s, tmp, ans, index + 2);
            tmp.pop_back();
        }
        if(index + 2 < s.size() && s.substr(index, 3) <= "255" && s.substr(index, 3) >= "100"){
            tmp.push_back(s.substr(index, 3));
            dfs(s, tmp, ans, index + 3);
            tmp.pop_back();
        }
    }
};
```

