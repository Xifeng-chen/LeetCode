### LeetCode每日一题——实现strStr()

> https://leetcode-cn.com/problems/implement-strstr/

```
//暴力法
class Solution
{
public:
    int strStr(string s, string p)
    {
        int n = s.size(), m = p.size();
        if(n == 0 && m != 0) return -1;//特判：当s为空并且p不为空的时候，返回-1
        if(m == 0) return 0; // 特判：当p为空的时候，返回0
        if(n == m) return s == p ? 0 : -1; //特判 当s和p长度相等的时候，如果s和p一样，就返回0，不一样，返回-1
        for(int i = 0; i <= n - m; i++){
        	int j = 0;
        	while(j < m && s[i] == p[j]){//对于每一个，进行匹配
        		i++, j++;
        	}
        	if(j == m) return i - j;
        	//如果j成功走到末尾，说明匹配成功，开始位置就是i - j
        	i -= j; // 恢复i的位置
        }
        return -1; //匹配失败
    }
};
```

```
//KMP算法
class Solution{
public:
	int strStr(string s, string p){
		int n = s.size(), m = p.size();
        if(n == 0 && m != 0) return -1;
        if(m == 0) return 0; 
        if(n == m) return s == p ? 0 : -1; 
        s.insert(s.begin(), ' ');
        p.insert(p.begin(), ' ');
        vector<int> next(m + 1);
        for(int i = 2, j = 0; i <= m; i++){//构造next数组
        	while(j and p[i] != p[j + 1]) j = next[j];
        	if(p[i] == p[j + 1]) j++;
        	next[i] = j;
        }
        for(int i = 1, j = 0; i <= n; i++){
        	while(j and s[i] != p[j + 1]) j = next[j];
        	//根据next数组，减少重复查找的次数
        	if(s[i] == p[j + 1]) j++;
        	if(j == m) return i - m;
        }
        return -1;
	}
};
```

