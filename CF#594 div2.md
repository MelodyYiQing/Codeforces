C题
<br>http://codeforces.com/contest/1248/problem/C
<br>solution:其实当时算一下，如果上一行有连续的两个相同颜色的色块的话，整张图就能确定了。所以我们先确定好第一行有多少种排列。
<br>图为n行m列
<br>然后其实使用dp写一下。dp[i][0]代表i号放白色色块，则dp[i][0]=dp[i-1][1]+dp[i-2][1] (也就是说如果放白色格子的话就需要前面一个是黑色或者前前黑前白)
<br>同理，dp[i][1]=dp[i-1][0]+dp[i-2][0]
<br>这里可以很神奇的发现dp[i][0]+dp[i][1]=dp[i-1][1]+dp[i-2][1]+dp[i-1][0]+dp[i-2][0].就是dp[i]=dp[i-1]+dp[i-2]
<br>然后我们知道黑白相间的可能只有两种01010101010...和1010101001...
<br>所以我们一开始可以确定的有连续块的图数就是dp[m]-2。
<br>然后考虑黑白相间的，这种情况下，下一行是不确定的。但是我们想到的是如果第一行确定了是黑白相间的话，我们只需要考虑列上会有多少种不同的排法满足条件
<br>这个时候，配上第一行就一定能够确定一张图，因为相连三格不能颜色相同嘛。
<br>所以最后的答案就是dp[m]+dp[n]-2,不要忘记取模！
```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;
int dp[100000+10];
int mod=1000000007;
int main()
{
    int n,m;
    cin>>n>>m;
    if(n<m) swap(n,m);
    dp[1]=2;
    dp[2]=4;
    for(int i=3;i<=n;++i) dp[i]=(dp[i-1]+dp[i-2])%mod;
    cout<<(dp[m]+dp[n]-2)%mod<<endl;
    return 0;
}
```
