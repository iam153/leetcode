洛谷p1060 开心的金明
之前做过几道dp，但这次看起来还是很陌生。可能是因为之前做的太少了，而且没有总结。dp种类可能很多，这篇就只总结背包问题相关。

以下问题中m为可选物品数量，n为总可用钱数，f[i][j]表示用j块钱在前i件物品中最多可以选到多少钱的物品。w[i]为i号物品的费用（体积），v[i]为i号物品的价值

打表调试代码  

```cpp
cout << " ";
	for (int i = 0; i <= m; i++)
		printf("%5d", i);
	cout << endl;
	for (int i = 0; i <= n; i++) {
		cout << p[i]; 
		for (int j = 0; j <= m; j++) {
			printf("%5d", f[i][j]);
		}; 
		cout << endl << endl;
	}
```

  
01背包，无优化
```cpp
for(int i = 1; i <= m; i++)
	for (int j = 0; j <= n; j++) {
		f[i][j] = f[i - 1][j];
		if(j >= w[i])
			f[i][j] = max(f[i - 1][j], v[i] + f[i - 1][j - w[i]]);
	}
cout << f[m][n];
```

一维数组空间优化  
这里注意内层循环的倒序就可以。可以优化的原因就是每一行的状态只与上一行的本格和之前某格(f[i - 1][j - w[i]])有关。因此可以优化空间
```cpp
for(int i = 1; i <= m; i++)
		for (int j = n; j >= 0; j--) {
			if(j >= w[i])
				f[j] = max(f[j], v[i] + f[j - w[i]]);
		}
	cout << f[n];
```
