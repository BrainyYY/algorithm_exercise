# **Exercise 1:**  

某设备工作时有A、B两个通道向外发射信号，每个通道发射信号的功率大小可单独由License控制，License可叠加使用但不能拆分，如将功率为2W和3W的License加载到设备控制A通道发射功率，则A通道可以5W的功率发射信号。用户现有N个功率大小不同的License，希望使设备的两个通道能够以最大并且相同的功率发射信号。  

**解答要求：**  
时间限制: C/C++ 100ms，其他语言: 200ms  
内存限制:C/C++32MB，其他语言：64MB  

**输入**  
第一行是用户现有License数量num，值的范围[0,50]  
第二行是num个整数的数组，数组元素的值表示License中功率大小，数组元素值的范围[0,50]

**输出**  
每个通道最大可能发射功率，如果无法分配则通道发射功率为0。  

**样例1:**  
输入:5  
2 4 6 8 10  
输出:14  
解释: 6+8=14，4+10=14，每个通道最大发射功率为14。  

**样例2:**  
输入:3  
1 2 4  
输出:0  
解释: 现有License无法实现合并分配到两个通道，使两个通道的功率相同。  

## **Code:**  

```cpp
#include<bits/stdc++.h>
using namespace std;
int dp[2520][2520];  // 1 int = 8byte; 1byte = 8 bits; 2520*2520*8/1024/1024~=23.84MB 
int main()
{
    int n;
    scanf("%d",&n);
    int dp[0][0]=1;
    int s=0;
    for(int i=1;i<=n;i++)
    {
        int x;
        scanf("%d",&x);
        for(int j=s;j>=0;j--)
            for(int k=s;k>=0;k--)
                if(dp[j][k])
                {
                   dp[j+x][k]=1; // actually it's bit value;
                   dp[j][k+x]=1;
                }
        s=s+x;
    }
    for(int i=s;i>=0;i--)
        if(dp[i][i])
        {
            printf("&d\n",i);
            return 0;
        }
}
```
