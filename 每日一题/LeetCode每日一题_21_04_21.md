### LeetCode每日一题——解码方法

> https://leetcode-cn.com/problems/decode-ways/

```
//动态规划
class Solution
{
public:
    int numDecodings(string s)
    {
        int len = s.size();
        if(len == 0) return 0;
        if(len == 1) return s == "0" ? 0 : 1;
        s = " " + s;
        vector<int> dp(len + 1, 0);
        dp[0] = 1;
        for(int i = 1; i <= len; i++){
        	int a = s[i] - '0', b = (s[i - 1] - '0') * 10 + s[i] - '0';
        	if(1 <= a && a <= 9) dp[i] += dp[i - 1];
        	if(10 <= b && b <= 26) dp[i] += dp[i - 2];
        }
        return dp[len];
    }
};
```

```
//动态规划
class Solution
{
public:
    int numDecodings(string s)
    {
        int len = s.size();
        if(len == 0) return 0;
        if(len == 1) return s == "0" ? 0 : 1;
        s = " " + s;
        int dp[3];
        memset(dp, 0, sizeof(dp));
        dp[0] = 1;
        for(int i = 1; i <= len; i++){
        	dp[i % 3] = 0;
        	int a = s[i] - '0', b = (s[i - 1] - '0') * 10 + s[i] - '0';
        	if(1 <= a && a <= 9) dp[i % 3] += dp[(i - 1) % 3];
        	if(10 <= b && b <= 26) dp[i % 3] += dp[(i - 2) % 3];
        }
        return dp[len % 3];
    }
};
```

```
int f[105];
class Solution
{
	public:
		int numDecodings(string s){
			int len = s.size();
            if(len == 0) return 0;
            if(len == 1) return s == "0" ? 0 : 1;
            memset(f, -1, sizeof(f));
            
            std::function<int(string, int)> dfs = [&](string ss, int idx){
            	if(ss.size() <= idx) return 1;
            	if(ss[idx] == '0') return 0;
            	if(f[idx] != -1) return f[idx];
            	int a = dfs(ss, idx + 1);
            	int b = 0;
            	if(stoi(ss.substr(idx, 2)) <= 26 && idx + 2 <= ss.size()){
            		b = dfs(ss, idx + 2);
            	}
            	f[idx] = a + b;
            }
            
            return dfs(s, 0);
		}
};
```

