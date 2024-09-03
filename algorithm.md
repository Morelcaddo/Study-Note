#  ASCII码

```
字符  ASCII码   字符  ASCII码   字符   ASCII码   字符   ASCII码
  A       65     a      97      0        48   空格        32
  B       66     b      98      1        49
  …       …
  Z       90     z     122      9        57
```



# scanf和printf

```
printf("%04d--%02d--%02d", 312, 2, 5);//第一个数代表要填充的数字，第二位表示显示多少位
printf("%.2f\n",3.154)//保留两位小数
```



# 费马定理

```
(a/b)%mod=a*(b)^(mod-2)%mod
```



# 前n项平方和公式

$$
n(n+1)(2n+1)/6
$$



# vector排序去重

```
vector<int>a;
sort(a.begin(),a.end());
a.erase(unique(a.begin(),a.end()),a.end());//unique把重复的放到最后，并返回第一个去重的元素
```



# auto相关

```
for(auto it:a)//只查看不允许修改
for(auto it:a)//允许修改
```



# 优先队列

```
priority_queue<int,vector<int>,greater<int>>//堆顶最小
priority_queue<int,vector<int>,less<int>>//堆顶最大
```



# map排序相关

```
map<string,int> m{{"a",1},{"b",2},{"c",3}};

vector<pair<string,int>> v(m.begin(),m.end());//将map中的元素拷贝到vector中

sort(v.begin(),v.end(),compare);//实现value的排序

```



# 字符串查找子串出现的所有位置

```
int main() 
{
    while (cin >> s >> c) 
    {
        int index = 0;//用来存储不断更新最新找到的位置
        int sum = 0;//累加出现的次数
        while ((index = s.find(c, index)) != string::npos) 
        {
            cout << "sum: " << sum + 1 << " index: " << index << endl;
            index += c.length();//上一次s中与c完全匹配的字符应跳过，不再比较
            sum++;
        }
        cout << sum << endl;
    }
}

```



# 树状数组(单点修改)

```
//lowbit(10010010)=(00000010)
//lowbit(x)=x&-x
//ti的管辖区间为(i-lowbit(i)+1,i),长度 lowbit(i)
//二进制优化思想

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 2e5 + 6;
int a[N];
ll t[N];
int n, q;

int lowbit(int x) 
{
    return (x & -x);
}

void update(int idx, int num)
{
    for (int i = idx; i <= n; i+=lowbit(i))
    {
        t[i] += num;
    }
}//给t[idx]加上num

ll getSum(int idx)
{
    ll res = 0;
    for (int i = idx; i > 0; i -= lowbit(i))
    {
        res += t[i];
    }
    return res;
}

int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    
    cin >> n >> q;

    for (int i = 1; i <= n; i++)
    {
        cin >> a[i];
        update(i, a[i]);
    }

    while (q--)
    {
        int op;
        cin >> op;
        if (op == 1)
        {
            int x, v;
            cin >> x >> v;
            update(x, v);
        }
        else
        {
            int l, r;
            cin >> l >> r;
            cout << getSum(r) - getSum(l - 1) << endl;
        }
    }
}
```



# 树状数组(区间修改）

```
//sum(l,r)公式，表示该公式进行累加从l到r
//sum(1,n)ai=(n+1)*sum(1,n)di-sum(1,n)i*di
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;

const int N = 2e5 + 3;
int a[N];
ll t1[N], t2[N];
int n, q;

int lowbit(int x) { return (x & -x); }

void update(int idx, int x)
{
	for (int i = idx; i <= n; i += lowbit(i))
	{
		t1[i] += x;
		t2[i] += (ll)idx * x;
	}
}

void insert(int l, int r, int x)
{
	update(l, x);
	update(r + 1, -x);
}



ll getsum(int idx)
{
	ll res = 0;
	for (int i = idx; i > 0; i -= lowbit(i))
	{
		res += ((ll)idx + 1) * t1[i] - t2[i];
	}
	return res;
}

int main()
{
	ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

	
	cin >> n >> q;
	for (int i = 1; i <= n; i++)
	{
		cin >> a[i];
		insert(i, i, a[i]);
	}


	while (q--)
	{
		int op;
		cin >> op;
		if (op == 1)
		{
			int l, r, v;
			cin >> l >> r >> v;
			insert(l, r, v);
		}
		else
		{
			int l, r;
			cin >> l >> r;
			cout << getsum(r) - getsum(l - 1) << "\n";
		}
	}
}
```



# 树状数组(计算逆序对)

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;

const int N = 2e5 + 3;
int n, a[N];
ll t[N];

vector<int>vec;

int B_S(int x)
{
	return lower_bound(vec.begin(), vec.end(), x) - vec.begin() + 1;
}

int lowbit(int x) { return (x & -x); }

void update(int idx, int x)
{
	for (int i = idx; i <= vec.size(); i += lowbit(i))
	{
		t[i] += x;
	}
}

ll getsum(int idx)
{
	ll res = 0;
	for (int i = idx; i > 0; i -= lowbit(i))
	{
		res += t[i];
	}
	return res;
}

int main()
{
	ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

	cin >> n;

	for (int i = 1; i <= n; i++)
	{
		cin >> a[i];
		vec.push_back(a[i]);
	}

	sort(vec.begin(), vec.end());
	vec.erase(unique(vec.begin(), vec.end()), vec.end());
	
	ll ans = 0;
	for (int i = 1; i <= n; i++)
	{
		int idx = B_S(a[i]);
		ans += (getsum(vec.size()) - getsum(idx));

		update(idx, 1);
	}

	cout << ans << "\n";
}

```



# 龟速乘

```
ll quick_mul(int a, int k)
{
	int ans = 0;
	while (k)
	{
		if (k & 1)ans = ((ll)ans + a) % mod;
		a = ((ll)a + a) % mod;
		k >>= 1;
	}
	return ans;
}
```

# 取消同步流

```
std::ios::sync_with_stdio(false),cin.tie(0),cout.tie(0);
```



# 龟速乘加快速幂

```
ll quick_pow(int a, int k)
{
	ll res = 1;
	while (k)
	{
		if (k & 1)res = quick_mul(res, a);
		a = quick_mul(a, a);
		k >>= 1;
	}
	return res;
}
```

# 快速乘

```
long long int a,b,mod;
cin>>a>>b>>mod;
cout<<((a*b-(long long )((long double)a*b/mod)*mod+mod)%mod);
```

# 取模公式

```
加法取模
(a+b)%mod=(a%mod+b%mod)%mod
减法取模
(a-b)%mod=(a%mod-b%mod+mod)%mod
乘法取模
(a*b)%mod=(a%mod*b%mod)%mod
(a^b) % p = ((a % p)^b) % p
除法取模
(a/b）%mod=(a/b*mod)%mod
```



# 字符串的数字转换成int类型的数字

```
long long int srtToDigint(string num)
{
	long long int ans = 0;
	for (int i = 0; i < num.size(); i++)
	{
		ans = ans * 10 + num[i] - '0';
	}
	return ans;
}
```



# 十进制转任意进制

```
string tenToX(long long num, int radix)
{
	string ans = "";
	do
	{
		int x = num % radix;
		if (x >= 0 && x < 10)
			ans = char('0' + x) + ans;
		else
			ans = char('A' + x - 10) + ans;
		num /= radix;
	} while (num);
	return ans;
}
```



# 任意进制转十进制

```
long long xToTen(string num, int radix)
{
    long long ans=0;
    for(int i=0;i<num.size();i++)
    {
        if(num[i]>='0'&&num[i]<='9')
            ans=ans*radix+num[i]-'0';
        else
            ans=ans*radix+num[i]-'A'+10;
    }
    return ans;
}
```



# 大整数取模

```
typedef long long int ll;
ll BigIntMod(string num, ll mod)
{
	ll ans = 0;
	for (int i = 0; i < num.size(); i++)
	{
		ans = ans * 10 + num[i] - '0';
		ans %= mod;
	}
	return ans;
}
```

# 回文串判断

```
bool isPal(string s)
{
    string ss=s;
    reverse(s.begin(),s.end());
    return ss==s;
}
```



# 闰年判定

```
bool f(int ye)
{
	if (ye % 4 == 0)
	{
		if (ye % 100 == 0 && ye % 400 != 0)
		{
			return false;
		}
		else if (ye % 3200 == 0)
		{
			return false;
		}
		else
		{
			return true;
		}
	}
	else
	{
		return false;
	}
}
```



# 快速排序

```
void quick_sort(int a[], int l, int r)
{
    if (l >= r)return;
    int i = l - 1;
    int j = r + 1;
    int x = a[(i + j) / 2];
    while (i < j)
    {
        do i++; while (a[i] < x);
        do j--; while (a[j] > x);
        if (i < j)swap(a[i], a[j]);
    }
    quick_sort(a, l, j);
    quick_sort(a, j + 1, r);
}
```



# 快速查找

```
int quick_search(int a[], int l, int r,int k)
{
    if (l >= r)return a[l];
    int i = l - 1;
    int j = r + 1;
    int x = a[(i + j) / 2];
    while (i < j)
    {
        do i++; while (a[i] < x);
        do j--; while (a[j] > x);
        if (i < j)swap(a[i], a[j]);
    }
    if (k <= j) quick_search(a, l, j, k);
    else quick_search(a, j + 1, r, k);
}
```



# 归并排序

    int tmp[N];
    
    void merge_sort(int q[], int l, int r)
    {
    	if (l >= r) return;
    
    	int mid = l + r >> 1;
    
    	merge_sort(q, l, mid), merge_sort(q, mid + 1, r);
    
    	int k = 0, i = l, j = mid + 1;
    
    	while (i <= mid && j <= r)
    	{
    		if (q[i] <= q[j]) tmp[k++] = q[i++];
    		else tmp[k++] = q[j++];
    	}
    
    	while (i <= mid) tmp[k++] = q[i++];
    	while (j <= r) tmp[k++] = q[j++];
    
    	for (i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];
    }

# 归并排序计算逆序对

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1e5 + 6;

int a[N], tmp[N];

ll merge_sort(int q[], int l, int r)
{
	if (l >= r) return 0;

	int mid = l + r >> 1;

	ll res=merge_sort(q, l, mid)+merge_sort(q, mid + 1, r);

	int k = 0, i = l, j = mid + 1;

	while (i <= mid && j <= r)
	{
		if (q[i] <= q[j]) tmp[k++] = q[i++];
		else
		{
			tmp[k++] = q[j++];
			res += mid - i + 1;
		}
	}

	while (i <= mid) tmp[k++] = q[i++];
	while (j <= r) tmp[k++] = q[j++];

	for (i = l, j = 0; i <= r; i++, j++) q[i] = tmp[j];

	return res;
}
int main()
{
    int n;
    scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &a[i]);
	}
	ll ans = merge_sort(a, 0, n - 1);
	printf("%lld", ans);
}
```



# 桶排序

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 2e5 + 6;
int a[N];



int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        int x;
        scanf("%d", &x);
        a[x]++;
    }

    for (int i = 0; i < 2e5 + 6; i++)
    {
        for (int j = 0; j < a[i]; j++)
        {
            printf("%d ", i);
        }
    }

}
```



# 二进制枚举

```
int main()
{
	int n;
	cin >> n;
	int* a = new int[n];
	for (int i = 0; i < n; i++)
	{
		cin >> a[i];
	}
	set<int>s;
	for (int i = 0; i < (1 << n); i++)
	{
		int cnt = i;
		int sum = 0;
		for (int j = 0; j < n; j++)
		{
			if (cnt & 1)
			{
				sum += a[j];
			}
			cnt >>= 1;
		}
		s.insert(sum);
	}
	cout << s.size() << endl;
	return 0;
}
```



# 二分查找

```
while (l < r)
{
	int mid = l + r + 1 >> 1;/*最小值最大化，小于等于目标条件的最大值*/
	// int mid = l + r >> 1;/*最大值最小化，大于等于目标条件的最小值*/
	if (check(mid))//条件
	{
		l = mid;
		// r = mid
	}
	else
	{
		r = mid - 1;
		// l = mid + 1;
	}
	//下拉不加，上拉加
}

//lower_bound(a.begin(),a.end(),num)-a.begin()查找大于等于目标值的最小的数,第四个参数greater<int>()加上大于变小于
//upper_bound(a.begin,a.end(),num)-a.begin()查找大于目标值的最小的数
```



# 字符串处理，stringstream

```
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int n;
	cin >> n;
	getchar();
	for (int i = 0; i < n; i++)
	{
		string s;
		getline(cin, s);
		cout << s << endl;
		cout << "AI:";
		for (int i = 0; i < s.length(); i++)
		{
			if (isalnum(s[i]))//isalnum()用来判断一个字符是否为数字或者字母，也就是说判断一个字符是否属于a~z||A~Z||0~9。
			{
				//把原文中所有大写英文字母变成小写，除了 I
				if (s[i] != 'I') s[i] = tolower(s[i]);
			}
			else {
				s.insert(i, " ");//对每个非字母和数字之前加空格
				i++;
			}
			if (s[i] == '?')s[i] = '!';
		}
		stringstream ss(s);//将s复制到ss字符串中
		string s1;
		vector<string> str;
		while (ss >> s1)//相当于输入一个个的单词，这样就可以消掉句子前的空格以及单词间多余的空格 
		{
			str.push_back(s1);
		}
		str.push_back("");//多向容器中加入一个元素，防止下面i+1溢出 
		if (!isalnum(str[0][0]))cout << " ";//若第一个字符串的第一个字符是符号，则需要先输出一个空格，因为题目要求"AI:"后面要有一个空格。
		for (int i = 0; i < str.size() - 1; i++)
		{
			string s2 = str[i];
			string ds = s2;
			if (!isalnum(s2[0]))ds.erase(0, 1);
			if (ds == "can" && str[i + 1] == "you")
			{//can和could前面可能会有符号 
				if (!isalnum(s2[0]))cout << s2[0];
				else cout << " ";
				cout << "I can";
				i++;
			}
			else if (ds=="could" && str[i + 1] == "you")
			{
				if (!isalnum(s2[0]))cout << s2[0];
				else cout << " ";
				cout << "I could";
				i++;
			}
			else if (str[i] == "I" || str[i] == "me") cout << " you";
			else if (!isalnum(str[i][0])) cout << str[i];
			else cout << " " << str[i];
		}
		cout << endl;
	}
	return 0;
}
```



# 高精度加法

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
vector<int>add(vector<int>& A, vector<int>& B)
{
	if (A.size() < B.size())return add(B, A);
	vector<int>C;
	int t = 0;
	for (int i = 0; i < A.size(); i++)
	{
		t += A[i];
		if (i < B.size())t += B[i];
		C.push_back(t % 10);
		t /= 10;
	}
	if (t)C.push_back(t);
	return C;
}
int main()
{
	string a, b;
	cin >> a >> b;
	vector<int>A, B;
	for (int i = a.size() - 1; i >= 0; i--)
	{
		A.push_back(a[i] - '0');
	}
	for (int i = b.size() - 1; i >= 0; i--)
	{
		B.push_back(b[i] - '0');
	}
	vector<int>C = add(A, B);
	for (int i = C.size() - 1; i >= 0; i--)
	{
		printf("%d", C[i]);
	}
}
```



# 高精度减法

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
bool cmp(vector<int> &A, vector<int> &B)
{
    if (A.size() != B.size()) return A.size() > B.size();

    for (int i = A.size() - 1; i >= 0; i -- )
        if (A[i] != B[i])
            return A[i] > B[i];

    return true;

}

vector<int> sub(vector<int> &A, vector<int> &B)
{
    vector<int> C;
    for (int i = 0, t = 0; i < A.size(); i ++ )
    {
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;

}

int main()
{
    string a, b;
    vector<int> A, B;
    cin >> a >> b;
    for (int i = a.size() - 1; i >= 0; i -- ) A.push_back(a[i] - '0');
    for (int i = b.size() - 1; i >= 0; i -- ) B.push_back(b[i] - '0');

    vector<int> C;

    if (cmp(A, B)) C = sub(A, B);
    else C = sub(B, A), cout << '-';

    for (int i = C.size() - 1; i >= 0; i -- ) cout << C[i];
    cout << endl;

    return 0;

}
```



# 高精度乘法

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
vector<int>mul(vector<int>& A, int B)
{
    vector<int>C;
    int t = 0;
    for (int i = 0; i < A.size()||t; i++)
    {
        if(i<A.size())t += A[i] * B;
        C.push_back(t % 10);
        t /= 10;
    }
    while (C.size() > 1 && C.back() == 0)C.pop_back();
    return C;
}
int main()
{
    string a;
    int b;
    cin >> a >> b;
    vector<int>A;
    for (int i = a.size() - 1; i >= 0; i--)A.push_back(a[i] - '0');
    vector<int>C=mul(A, b);
    for (int i = C.size() - 1; i >= 0; i--)
    {
        printf("%d", C[i]);
    }
}
```



# 高精度除法

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e6 + 5;
vector<int>div(vector<int>& A, int B,int& t)
{
    vector<int>C;
    t = 0;
    for (int i = A.size() - 1; i >= 0; i--)
    {
        t = t * 10 + A[i];
        C.push_back(t / B);
        t %= B;
    }
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0)C.pop_back();
    return C;
}
int main()
{
    string a;
    int b;
    cin >> a >> b;
    vector<int>A;
    for (int i = a.size() - 1; i >= 0; i--)A.push_back(a[i] - '0');
    int t;
    auto C = div(A, b, t);
    for (int i = C.size() - 1; i >= 0; i--)
    {
        printf("%d", C[i]);
    }
    cout << endl << t;
}
```



# 一维前缀和

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 5;
int a[N] = {0};
int b[N] = {0};
int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &a[i]);
        b[i] = b[i - 1] + a[i];
    }
    while (m--)
    {
        int l, r;//要计算的区间和
        scanf("%d%d", &l, &r);
        cout << b[r] - b[l - 1] << endl;
    }
}
```



# 二维前缀和

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e3 + 5;
int a[N][N] = {0};//前缀和数组
int main()
{
    int n, m, q;
    scanf("%d%d%d", &n, &m, &q);
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            scanf("%d", &a[i][j]);
            a[i][j] += (a[i - 1][j] + a[i][j - 1] - a[i - 1][j - 1]);
        }
    }
    while (q--)
    {
        int x1, y1, x2, y2;
        scanf("%d%d%d%d", &x1, &y1, &x2, &y2);//待求的二维数组的范围
        cout << a[x2][y2] - a[x1 - 1][y2] - a[x2][y1 - 1] + a[x1 - 1][y1 - 1] << endl;
    }
}
```



# 一维差分

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e6 + 5;
int a[N] = { 0 };//原数组（把原数组当作一个前缀和数组）
int b[N] = { 0 };//差分数组
void insert(int l, int r, int c)
{
    b[l] += c;
    b[r + 1] -= c;
}
int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
    {
        scanf("%d", &a[i]);
        insert(i, i, a[i]);
    }
    while (m--)
    {
        int l, r, c;//待差分区间，以及要加的数
        scanf("%d%d%d", &l, &r, &c);
        insert(l, r, c);
    }
    for (int i = 1; i <= n; i++)
    {
        b[i] += b[i - 1];
        printf("%d ", b[i]);
    }
}
```



# 二维差分

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e3 + 5;
int a[N][N] = { 0 };//原数组
int b[N][N] = { 0 };//差分数组
void insert(int x1, int y1, int x2, int y2, int c)
{
    b[x1][y1] += c;
    b[x2 + 1][y1] -= c;
    b[x1][y2 + 1] -= c;
    b[x2 + 1][y2 + 1] += c;
}
int main()
{
    int n, m, q;
    scanf("%d%d%d", &n, &m, &q);
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            scanf("%d", &a[i][j]);
            insert(i, j, i, j, a[i][j]);
        }
    }
    while (q--)
    {
        int x1, y1, x2, y2, c;//待差分的区间以及要加的数
        scanf("%d%d%d%d%d", &x1, &y1, &x2, &y2, &c);
        insert(x1, y1, x2, y2, c);
    }
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            b[i][j] += b[i - 1][j] + b[i][j - 1] - b[i - 1][j - 1];
            printf("%d ", b[i][j]);
        }
        printf("\n");
    }
}
```



# 双指针

```
//最长连续不重复子序列

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 5;
int a[N];
int cnt[N];
int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    int ans = 0;
    for (int i = 0, j = 0; i < n; i++)
    {
        cnt[a[i]]++;
        while (j < i && cnt[a[i]]>1)cnt[a[j++]]--;//j < i可以不需要
        ans = max(ans, i - j + 1);
    }
    printf("%d", ans);
}



//数组元素的目标和

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 5;
int a[N] = { 0 };
int b[N] = { 0 };
int main()
{
    int n, m, x;
    scanf("%d%d%d", &n, &m, &x);
    map<int, int>cnt;
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
        cnt[a[i]]++;
    }
    int ans1;
    int ans2;
    for (int i = 0; i < m; i++)
    {
        scanf("%d", &b[i]);
        if (cnt[x - b[i]]) 
        {
            ans2 = i;
            for (int j = 0; j < n; j++)
            {
                if (a[j] == x - b[i])
                {
                    ans1 = j;
                }
            }
        }
    }
    cout << ans1 << " " << ans2;
}

//判断子序列（判断a是否为b的非连续子序列）
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 5;
int a[N] = { 0 };
int b[N] = { 0 };
int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }
    for (int i = 0; i < m; i++)
    {
        scanf("%d", &b[i]);
    }
    int i = 0;
    int j = 0;
    while (i < n && j < m)
    {
        if (a[i] == b[j])i++;
        j++;
    }
    if (i == n)cout << "Yes";
    else cout << "No";
}
```



# 离散化

```
//区间和
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 3e5 + 6;
vector<pair<int, int>>alldata,section;
vector<int>vec;
int a[N];
int s[N];
int binary_search(int x)
{
    int l = 0;
    int r = vec.size() - 1;
    while (l < r)
    {
        int mid = (l + r) >> 1;
        if (vec[mid] >= x)
        {
            r = mid;
        }
        else
        {
            l = mid + 1;
        }
    }
    return l + 1;
}
int main()
{
    int n, m;
    scanf("%d%d", &n, &m);
    while (n--)
    {
        int x, c;
        scanf("%d%d", &x, &c);
        alldata.push_back({ x,c });
        vec.push_back(x);
    }
    while (m--)
    {
        int l, r;
        scanf("%d%d", &l, &r);
        section.push_back({ l,r });
        vec.push_back(l);
        vec.push_back(r);
    }
    sort(vec.begin(), vec.end());
    vec.erase(unique(vec.begin(),vec.end()), vec.end());
    for (auto it : alldata)
    {
        int x = binary_search(it.first);
        a[x] += it.second;
    }
    for (int i = 1; i <= vec.size(); i++)
    {
        s[i] = s[i - 1] + a[i];
    }
    for (auto it : section)
    {
        int l = binary_search(it.first);
        int r = binary_search(it.second);
        printf("%d\n", s[r] - s[l - 1]);
    }
}
```



# 区间合并

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 3e5 + 6;
vector<pair<int, int>>section;
vector<pair<int, int>>ans;
int main()
{
    int n;
    scanf("%d", &n);
    while (n--)
    {
        int l, r;
        scanf("%d%d", &l, &r);
        section.push_back({ l,r });
    }
    sort(section.begin(), section.end());
    int st = section[0].first;
    int end = section[0].second;
    for (int i = 1; i < section.size(); i++)
    {
        if (section[i].first > end)
        {
            ans.push_back({ st,end });
            st = section[i].first;
            end = section[i].second;
        }
        else
        {
            end = max(section[i].second, end);
        }
    }
    ans.push_back({ st,end });
    printf("%d", ans.size());
}
```



# 单链表

```
const int N = 2e5 + 5;
int head, val[N], ne[N], idx;
void init()
{
    head = -1;
    idx = 0;
}
void add_head(int num)
{
    val[idx] = num;
    ne[idx] = head;
    head = idx++;
}
void add(int k, int num)//加入到第k个数的后面
{
    val[idx] = num;
    ne[idx] = ne[k - 1];
    ne[k - 1] = idx++;
}
void remove(int k)//删除第k个插入数后面的那个数
{
    ne[k - 1] = ne[ne[k - 1]];
}
void display()
{
	for (int i = head; i != -1; i = ne[i])
	{
		cout << val[i] << " ";
	}
}
```



# 双链表

```
const int N;
int head, val[N], l[N], r[N], idx;
void init()
{
    r[0] = 1;
    l[1] = 0;
    idx = 2;
}
void add(int k, int num)
{
    val[idx] = num;
    r[idx] = r[k];
    l[idx] = k;
    l[r[k]] = idx;
    r[k] = idx++;
}
void remove(int k)
{
    l[r[k]] = l[k];
    r[l[k]] = r[k];
}
void display()
{
	for (int i = r[0]; i != 1; i = r[i])
	{
		cout << val[i] << " ";
	}
}
```



# 模拟栈

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 5;
int stk[N];
int idx;
int main()
{
    idx = 0;
    int m;
    cin >> m;
    while (m--)
    {
        string op;
        cin >> op;
        if (op == "push")
        {
            int x;
            cin >> x;
            stk[++idx] = x;
        }
        else if (op == "pop")
        {
            idx--;
        }
        else if (op == "empty")
        {
            if (idx == 0)
            {
                cout << "YES\n";
            }
            else
            {
                cout << "NO\n";
            }
        }
        else if (op == "query")
        {
            cout << stk[idx] << endl;
        }
    }
}
```



# 表达式求值

```
#include<unordered_map>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
stack<int>num;
stack<char>op;
void eval()
{
    int b = num.top(); num.pop();
    int a = num.top(); num.pop();
    char c = op.top(); op.pop();
    if (c == '+')
    {
        num.push(a + b);
    }
    else if (c == '-')
    {
        num.push(a - b);
    }
    else if (c == '*')
    {
        num.push(a * b);
    }
    else if (c == '/')
    {
        num.push(a / b);
    }
}
int main()
{
    unordered_map<char, int>pr{ {'+', 1}, {'-', 1}, {'*', 2}, {'/', 2} };
    string s;
    cin >> s;
    for (int i = 0; i < s.size(); i++)
    {
        if (isdigit(s[i]))
        {
            int x = 0;
            int j = i;
            while (j < s.size() && isdigit(s[j]))
            {
                x = x * 10 + s[j++] - '0';
            }
            i = j - 1;
            num.push(x);
        }
        else if (s[i] == '(')
        {
            op.push(s[i]);
        }
        else if (s[i] == ')')
        {
            while (op.top() != '(')eval();
            op.pop();
        }
        else
        {
            while (op.size() && op.top() != '(' && pr[op.top()] >= pr[s[i]])eval();
            op.push(s[i]);
        }
    }
    while (op.size())eval();
    cout << num.top();
}
```



# 模拟队列

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 6;
int q[N];
int hh = 0;
int tt = -1;
int main()
{
    int m;
    cin >> m;
    while (m--)
    {
        string op;
        cin >> op;
        if (op == "push")
        {
            int x;
            cin >> x;
            q[++tt] = x;
        }
        else if (op == "empty")
        {
            if (tt < hh)
            {
                cout << "YES\n";
            }
            else
            {
                cout << "NO\n";
            }
        }
        else if (op == "query")
        {
            cout << q[hh] << endl;
        }
        else if (op == "pop")
        {
            hh++;
        }
    }
}
```



# 单调栈

```
//给定一个长度为 N 的整数数列，输出每个数左边第一个比它小的数，如果不存在则输出 −1。
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e5 + 6;
int idx = 0;
int stk[N];
int main()
{
    int n;
    scanf("%d", &n);
    int x;
    while (n--)
    {
        scanf("%d", &x);
        while(idx && stk[idx] >= x)idx--;
        //针对当前的数字来说，首先是寻找栈里有没有比他小的数，有就立即输出，对于后面的数来说，
        //他们的左边的最小的数无非就两种选择，一种是栈里的元素，一种就是当前的元素，那我们是不是可以拿当前元素对栈内的
        //元素进行比较，判断究竟是栈里的更大，还是待插入的数更大，从而筛掉一部份数，而所有较小的数中，符合条件的一定是最后
        //一个进入栈的元素，即栈顶元素
        if (idx)cout << stk[idx] << " ";
        else cout << "-1 ";
        stk[++idx] = x;
    }
}
```



# 滑动窗口

```
//输出滑动窗口中元素的最大值和最小值
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef unsigned long long ull;
const int N = 1e6 + 6;
int a[N], q[N];
int main()
{
    int n, k;
    scanf("%d%d", &n, &k);

    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
    }

    int hh = 0;
    int tt = -1;
    for (int i = 0; i < n; i++)
    {
        if (hh <= tt && q[hh] < i - k + 1)hh++;
        while (hh <= tt && a[q[tt]] >= a[i])tt--;//最小值
        //窗口里的元素和队列的元素不一样，队列只保存可能符合答案筛选过后的数
        q[++tt] = i;
        if (i >= k - 1)printf("%d ", a[q[hh]]);
    }

    printf("\n");

    hh = 0;
    tt = -1;
    for (int i = 0; i < n; i++)
    {
        if (hh <= tt && q[hh] < i - k + 1)hh++;
        while (hh <= tt && a[q[tt]] <= a[i])tt--;//最大值
        q[++tt] = i;
        if (i >= k - 1)printf("%d ", a[q[hh]]);
    }
}
```



# 单调栈应用

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 1e5 + 3;
int st[N], idx, a[N], l[N], r[N];

int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++)cin >> a[i];

    for (int i = 1; i <= n; i++)
    {
        while (idx && a[st[idx]] >= a[i])idx--;

        if (idx)l[i] = st[idx];
        else l[i] = 0;
        
        st[++idx] = i;
    }

    idx = 0;
   
    for (int i = n; i >= 1; i--)
    {
        while (idx && a[st[idx]] > a[i])idx--;

        if (idx)r[i] = st[idx];
        else r[i] = n + 1;
        st[++idx] = i;
    }
    
    ll ans = 0;

    for (int i = 1; i <= n; i++)
    {
        ans += (a[i] * (ll)(i - l[i]) * (r[i] - i));
    }

    cout << ans << '\n';
}
//https://cdn.oj.eriktse.com/problem.php?id=1093
```



# KMP

```
//首先是构造next数组
//双指针i,j,对于待匹配字串，i先跑寻找后缀，j后跑寻找前缀，如果当前j指向的字符的下一位可以与后缀匹配上，就用next数组记录下当前j的值
如果不行，则回退到上次匹配成功的地方，然后重复改操作步骤
为什么kmp可以极大程度上优化时间，我们举一个例子abcdfabc,此时我们匹配到c发现不行，如果暴力做法我们要直接回退到这个字符串的起始位置，但是我们发现了一个事情，s(0-2)与s(5-7)相等，5,6可以匹配上，则证明，0 1也可以匹配上，那我们只需要从下标2开始重新匹配即可，对于i也是同理，如果j不需要回溯到最开始位置，i也不用回溯，i,j回溯同步
关于j=next[j],如果当前前后缀匹配失败，我们需要做什么？我们需要拿着当前这段前缀里面有没有跟当前后缀匹配上的部分，顺着这一部分继续衍生寻找新的前缀。相当于对当前所出现的前缀进行一个检索，在这之前的部分里面有没有可以衍生的相等前后缀

#include<bits/stdc++.h>

using namespace std;

const int N = 1000010;

int n, m;

int ne[N];
int main()
{
    string p, s;
    cin >> m >> p >> n >> s;

    ne[0] = -1;
    for (int i = 1, j = -1; i < p.size(); i++)
    {
        while (j != -1 && p[j + 1] != p[i]) j = ne[j];
        if (p[j + 1] == p[i]) j++;
        ne[i] = j;
    }

    for (int i = 0, j = -1; i < s.size(); i++)
    {
        while (j != -1 && s[i] != p[j + 1]) j = ne[j];
        if (s[i] == p[j + 1]) j++;
        if (j == p.size()-1)
        {
            cout << i - j << ' ';
            j = ne[j];
        }
    }

    return 0;
}
```



# Trie（字典树）

```
//高校的存储和查找字符串集合的数据结构
//.变量id： id代表字典树中每一个节点的编号，id的大小只与插入字典树的先后顺序有关，它的作用在下面会讲到。

//2.trie[N][26]： 每个trie代表一条边，字典树其中1~N为边上方节点的编号，0代表root节点，1~26为连在i节点下方的26个字母。如果trie[i][x]=0,则代表字典树中目前没有这个点，而trie[i][x]的值代表这个点下方连有的点的编号，例如：trie[i][2]=9代表第i号点和的下方连有一个点‘c’，并且那个点的编号是9，为什么是c呢？因为 ‘c’-‘a’=2

//3.cnt[N]: cnt[i]==0代表编号为i的点不是一个单词的结束点，在上面的图中代表这个点不是空点，但是没有标红，cnt[i]！=0代表编号为i的点是一个单词的结束点，即红点。cnt[i]不一定只为0或1，因为有可能多次输入了同一个单词。

#include<bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;
 
int trie[N][26],cnt[N],idx;//字典树数组，记录单词出现次数，结点标号

void insert(string str)
{
    int p = 0;
    for (int i = 0; i < str.size(); i++)
    {
        int u = str[i] - 'a';
        if (!trie[p][u])trie[p][u] = ++idx;
        p = trie[p][u];
    }
    cnt[p]++;
}

int query(string str)
{
    int p = 0;
    for (int i = 0; i < str.size(); i++)
    {
        int u = str[i] - 'a';
        if (!trie[p][u]) return 0;
        p = trie[p][u];
    }
    return cnt[p];
}

int main()
{
    int n;
    scanf("%d", &n);
    while (n--)
    {
        string op, s;
        cin >> op >> s;
        if (op == "I")insert(s);
        else printf("%d\n", query(s));
    }
    return 0;
}
```



# 最大异或对（字典树）

```
#include<bits/stdc++.h>

using namespace std;

const int N = 1e5 + 10;
const int M = 3e6 + 10;

int a[N];
int trie[M][2],idx;//字典树数组，记录单词出现次数，结点标号

void insert(int num)
{
    int p = 0;
    for (int i = 30; i >= 0; i--)
    {
        if (!trie[p][num >> i & 1])trie[p][num >> i & 1] = ++idx;
        p = trie[p][num >> i & 1];
    }
}

int query(int num)
{
    int p = 0, res = 0;
    for (int i = 30; i >= 0; i--)
    {
        if (trie[p][!(num >> i & 1)])
        {
            res += 1 << i;
            p = trie[p][!(num >> i & 1)];
        }
        else
        {
            p = trie[p][num >> i & 1];
        }
    }
    return res;
}

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++)
    {
        scanf("%d", &a[i]);
        insert(a[i]);
    }
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        ans = max(ans, query(a[i]));
    }
    printf("%d", ans);
    return 0;
}
```



# 并查集

```
const int N = 100010;

int fa[N];
//cnt[N];计数
void init()
{
    for (int i = 1; i <= n; i++)
    {
        fa[i] = i;
        //cnt[i] = 1;
    }
}

int find(int x)
{
    if (fa[x] != x) fa[x] = find(fa[x]);
    return fa[x];
}

void unin(int a,int b)
{
    fa[find(a)] = find(b);
    /*if (find(a) != find(b))
    {
        fa[find(a)] = find(b);
        cnt[find(b)] += cnt[find(a)];
    }*/
}
```



# 并查集（应用）

```
#include<bits/stdc++.h>//食物环问题
using namespace std;
typedef unsigned long long ll;
const int N = 5e4 + 6;
int fa[N];
int dis[N];//记录距离通过距离进行判断
int n, k;
void init()
{
    for (int i = 1; i <= n; i++)
    {
        fa[i] = i;
    }
}
int find(int x)
{
    if (fa[x] != x) 
    {
        int t = find(fa[x]);
        dis[x] += dis[fa[x]];
        fa[x] = t;
    }
    return fa[x];
}
void unin(int a,int b)
{
    fa[find(a)] = find(b);
}
int main()
{
    //0同类，1吃，2被吃
    scanf("%d%d", &n, &k);
    init();
    int ans = 0;
    while (k--)
    {
        int d, x, y;
        scanf("%d%d%d", &d, &x, &y);
        if (x > n || y > n)
        {
            ans++;
        }
        else
        {
            int px = find(x), py = find(y);
            if (d == 1)
            {
                if (px == py && (dis[x] - dis[y]) % 3)ans++;
                else if (px != py)
                {
                    unin(x, y);
                    dis[px] = dis[y] - dis[x];
                }
            }
            else
            {
                if (px == py&& (dis[x] - dis[y] - 1) % 3)ans++;
                else if (px != py)
                {
                    unin(x, y);
                    dis[px] = dis[y] - dis[x] + 1;
                }
            }
        }
    }
    printf("%d\n", ans);
    return 0;
}
```



# 堆排序

```
堆：一个完全二叉树，父节点小于等于两个根节点//下标从1开始 
设当前结点的标号为x，则该节点的右儿子为2*x+1，左儿子为2*x
down操作：数据的下沉操作
up操作：数据的上浮操作
关于堆的一些操作，插入，求最小值，删除
插入：insert(),heap[++size]=x; up(size);先将数据插入到最后一个结点，然后进行上浮操作
最小值：输出头结点的值即可
删除最小值，将最后一个结点的值覆盖给头节点，然后删除尾结点，在进行下沉操作，heap[1]=heap[size];size--;down(size)；
删除任意元素：同上，heap[k]=heap[size];size--;down(k);up(k);
修改任意一个元素：
//堆排序代码
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ll;
const int N = 1e5 + 10;
int n, m;
int heap[N], hsize;
void down(int u)
{
    int t = u;
    if (u * 2 <= hsize && heap[u * 2] < heap[t])t = u * 2;
    if (u * 2 + 1 <= hsize && heap[u * 2 + 1] < heap[t])t = u * 2 + 1;
    if (u != t)
    {
        swap(heap[u], heap[t]);
        down(t);
    }
}
void hdelete(int u)
{
    heap[u] = heap[hsize];
    hsize--;
    down(u);
}
int main()
{
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)scanf("%d", &heap[i]);

    hsize = n;

    for (int i = n / 2; i; i--)
    {
        down(i);
    }

    while (m--)
    {
        printf("%d ", heap[1]);
        hdelete(1);
    }
    return 0;
}

```



# 模拟堆

```
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ll;
const int N = 1e5 + 10;
int n, hsize, cnt;
int heap[N], hp[N], ph[N];//堆，堆中第k个点是第几个插入点，第k个数在堆中的下标
//代码中的第k个数均指插入顺序下的第k个数
void heap_swap(int a, int b)
{
    swap(ph[hp[a]], ph[hp[b]]);
    swap(hp[a], hp[b]);
    swap(heap[a], heap[b]);
}
void up(int u)
{
    while (u / 2 && heap[u] < heap[u / 2])
    {
        heap_swap(u, u / 2);
        u >>= 1;
    }
}
void down(int u)
{
    int t = u;
    if (u * 2 <= hsize && heap[u * 2] < heap[t])t = u * 2;
    if (u * 2 + 1 <= hsize && heap[u * 2 + 1] < heap[t])t = u * 2 + 1;
    if (u != t)
    {
        heap_swap(u, t);
        down(t);
    }
}
void hdelete(int u)
{
    heap_swap(u, hsize);
    hsize--;
    up(u);
    down(u);
}
int main()
{
    scanf("%d", &n);
    while (n--)
    {
        string op;
        cin >> op;
        if (op == "I")//插入一个数
        {
            int num;
            cin >> num;
            hsize++;
            cnt++;
            ph[cnt] = hsize;
            hp[hsize] = cnt;
            heap[hsize] = num;
            up(hsize);
        }
        else if (op == "PM")//输出最小值
        {
            cout << heap[1] << endl;
        }
        else if (op == "DM")//删除最小值
        {
            hdelete(1);
        }
        else if (op == "D")//删除第k个数
        {
            int k;
            scanf("%d", &k);
            k = ph[k];
            hdelete(k);
        }
        else//修改第k个数
        {
            int k, x;
            scanf("%d%d", &k, &x);
            k = ph[k];
            heap[k] = x;
            up(k);
            down(k);
        }
    }
    return 0;
}
```



# 模拟Hash表

```
#include<bits/stdc++.h>//基于链表实现的散列表，核心在于每个Hash槽位对应一个链表，代表该对应值下的所有数
using namespace std;
typedef unsigned long long ll;
const int N = 1e5 + 3;
int n;
int value[N], ne[N], qhash[N], idx;

void insert(int x)
{
    int k = (x % N + N) % N;//Hash函数
    value[idx] = x;//链表实现
    ne[idx] = qhash[k];
    qhash[k] = idx++;
}

bool find(int x)
{
    int k = (x % N + N) % N;
    for (int i = qhash[k]; i!=- 1; i = ne[i])
    {
        if (value[i] == x)
        {
            return true;
        }
    }
    return false;
}
int main()
{
    scanf("%d", &n);
    memset(qhash, -1, sizeof(qhash));//链表头赋值为1
    while (n--)
    {
        string op;
        cin >> op;
        int x;
        scanf("%d", &x);
        if (op == "I")
        {
            insert(x);
        }
        else
        {
            if (find(x))
            {
                printf("Yes\n");
            }
            else
            {
                printf("No\n");
            }
        }
    }
    return 0;
}
```



# 字符串hash

```
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;

const int N = 1e5 + 10;
const int P = 131;//将字符串的值转化为p进制的数
int n, m;
ull qhash[N], p[N];
void init(string s)
{
    p[0] = 1;
    for (int i = 1; i < s.size(); i++)
    {
        qhash[i] = qhash[i - 1] * P + s[i];//进制转换
        p[i] = p[i - 1] * P;//记录p的多少次方
    }
}

ull get(int l, int r)
{
    return qhash[r] - qhash[l - 1] * p[r - l + 1];//返回hash值，后半段要进行进制对齐
}

int main()
{
    scanf("%d%d", &n, &m);
    string s;
    cin >> s;

    s = " " + s;

    
    init(s);


    while (m--)
    {
        int l1, r1, l2, r2;
        scanf("%d%d%d%d", &l1, &r1, &l2, &r2);
        if (get(l1, r1) == get(l2, r2))printf("Yes\n");
        else printf("No\n");
    }
    return 0;
}
```



# 全排列（STL函数实现）

```
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;

const int N = 7;
int num[N];
int n;
int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		num[i] = i + 1;
	}
	do
	{
		for (int i = 0; i < n; i++)printf("%d ", num[i]);
		printf("\n");
	}while(next_permutation(num, num + n));//对目标数组中的前n个数进行全排列，需注意排列前，数组必须进行升序排序
}
```



# 全排列（其他用法）

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 1e4 + 5;
int a[N];
int n, m;


int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

    cin >> n >> m;

    for (int i = 0; i < n; i++)cin >> a[i];

    for (int i = 1; i <= m; i++)
    {
        next_permutation(a, a + n);
    }

    for (int i = 0; i < n; i++)
    {
        cout << a[i] << " ";
    }

}
```



# 全排列（DFS）

```
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;

const int N = 7;
int path[N];//记录当前选择
bool flag[N + 1];//回溯用，标记
int n;
void dfs(int step)
{
	if (step == n)
	{
		for (int i = 0; i < n; i++)printf("%d ", path[i]);
		printf("\n");
	}
	for (int i = 1; i <= n; i++)
	{
		if (!flag[i])
		{
			flag[i] = 1;
			path[step] = i;
			dfs(step + 1);
			flag[i] = false;
		}
	}
}
int main()
{
	scanf("%d", &n);
	dfs(0);
}

```



# DFS(n-皇后问题优化做法)

```
//n个皇后放在n×n的国际象棋棋盘上，使得皇后不能相互攻击到，即任意两个皇后都不能处于同一行、同一列或同一斜线上。
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;

const int N = 12;

int n;

bool col[N], dg[N], udg[N];

char qmap[N][N];
void dfs(int row)//搜索行数
{
	if (row == n)
	{
		for (int i = 0; i < n; i++)printf("%s\n", qmap[i]);
		puts("");
		return;
	}
	for (int i = 0; i < n; i++)//遍历列数
	{
		if (!col[i] && !dg[row + i] && !udg[n - row + i])
		{
			qmap[row][i] = 'Q';
			col[i] = dg[row + i] = udg[n - row + i] = true;
			dfs(row + 1);
			col[i] = dg[row + i] = udg[n - row + i] = false;
			qmap[row][i] = '.';
		}
	}
}

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			qmap[i][j] = '.';
		}
	}
	dfs(0);
}
```



# DFS（n-皇后问题暴力搜索做法）

```
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ull;
//x行y列

const int N = 12;

int n;

bool row[N],col[N], dg[N], udg[N];

char qmap[N][N];
void dfs(int x,int y,int step)
{
	if (y == n)y = 0, x++;
	if (x == n)
	{
		if (step == n)
		{
			for (int i = 0; i < n; i++)
			{
				printf("%s\n", qmap[i]);
			}
			puts("");
		}
		return;
	}
	dfs(x, y + 1, step);//不放皇后

	if (!row[x] && !col[y] && !dg[x + y] && !udg[x - y + n])//放皇后
	{
		qmap[x][y] = 'Q';
		row[x] = col[y] = dg[x + y] = udg[x - y + n] = true;
		dfs(x, y + 1, step + 1);
		row[x] = col[y] = dg[x + y] = udg[x - y + n] = false;
		qmap[x][y] = '.';
	}
}

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			qmap[i][j] = '.';
		}
	}
	dfs(0, 0, 0);
}
```



# BFS(模拟队列实现)

```
#include<bits/stdc++.h>//权重为1时，可以求得最短路径

using namespace std;

typedef unsigned long long ull;
typedef pair<int, int>PII;

const int N = 105;
int n, m;

int qmap[N][N];//存图
int d[N][N];//存的是每一个点到起点的距离
int dir[4][2] = { 1,0,-1,0,0,1,0,-1 };//向量函数
PII q[N * N];//模拟队列数组


int BFS()
{
	int hh = 0, tt = -1;//头指针，尾指针
	q[++tt] = { 0,0 };//放入起点
	
	memset(d, -1, sizeof(d));//全部赋值为-1，所有-1的点代表该点没有被搜索到

	d[0][0] = 0;//起点距离更新为0

	while (hh <= tt)//判断队列是否为空
	{
		auto t = q[hh++];//取出队首元素
		for (int i = 0; i < 4; i++)
		{
			int x = t.first + dir[i][0];
			int y = t.second + dir[i][1];
			if (x >= 0 && y >= 0 && x < n && y < m && !qmap[x][y] && d[x][y] == -1)
			{
				d[x][y] = d[t.first][t.second] + 1;//距离+1
				q[++tt] = { x,y };//将新搜索到的点放入队列
			}
		}
	}

	return d[n - 1][m - 1];
}

int main()
{
	scanf("%d%d", &n, &m);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			scanf("%d", &qmap[i][j]);
		}
	}
	
	printf("%d\n", BFS());
	
}
```



# BFS(STL队列实现)

```
#include<bits/stdc++.h>

using namespace std;

typedef unsigned long long ull;
typedef pair<int, int>PII;

const int N = 105;
int n, m;

int qmap[N][N];//存图
int d[N][N];//存的是每一个点到起点的距离
int dir[4][2] = { 1,0,-1,0,0,1,0,-1 };
queue<PII>q;


int BFS()
{
	q.push({ 0,0 });
	
	memset(d, -1, sizeof(d));

	d[0][0] = 0;

	while (q.size())
	{
		auto t = q.front();
		q.pop();
		for (int i = 0; i < 4; i++)
		{
			int x = t.first + dir[i][0];
			int y = t.second + dir[i][1];
			if (x >= 0 && y >= 0 && x < n && y < m && !qmap[x][y] && d[x][y] == -1)
			{
				d[x][y] = d[t.first][t.second] + 1;
				q.push({ x,y });
			}
		}
	}

	return d[n - 1][m - 1];
}

int main()
{
	scanf("%d%d", &n, &m);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			scanf("%d", &qmap[i][j]);
		}
	}
	
	printf("%d\n", BFS());
	
}
```



# BFS(八数图问题)

```
#include<bits/stdc++.h>
#include<unordered_map>
//核心思路是搜索每一种图的状态
using namespace std;

int dir[4][2] = { 1,0,-1,0,0,1,0,-1 };//方向数组



int BFS(string s)
{
	queue<string>q;
	unordered_map<string, int>dis;//记录距离

	q.push(s);
	dis[s] = 0;


	while (q.size())
	{
		auto t = q.front();
		q.pop();

		string end = "12345678x";

		if (t == end)return dis[t];
		int distance = dis[t];

		int k = t.find('x');

		int x = k / 3;//提取坐标值
		int y = k % 3;//提取坐标值

		for (int i = 0; i < 4; i++)
		{
			int tx = x + dir[i][0];
			int ty = y + dir[i][1];
			if (tx >= 0 && tx < 3 && ty >= 0 && ty < 3)
			{
				swap(t[k], t[tx * 3 + ty]);//坐标值转换回去
				if (!dis.count(t))
				{
					dis[t] = distance + 1;//距离刷新
					q.push(t);//记录状态
				}
				swap(t[k], t[tx * 3 + ty]);//状态恢复
			}
		}
	}
	return -1;
}

int main()
{
	string s;
	char c;
	for (int i = 0; i < 9; i++)
	{
		cin >> c;
		s = s + c;
	}
	cout << BFS(s) << endl;
}
```



# 树与图

```
树是无环连通图
图分有向图和无向图
有向图的邻接矩阵 qmap[a][b]存储a到b的边的权重
有向图的邻接表（链表）也可以用vector实现
重心定义：重心是指树中的一个结点，如果将这个点删除后，剩余各个连通块中点数的最大值最小，那么这个节点被称为树的重心。
```



# 树与图的DFS(树的中心寻找)

```
#include<bits/stdc++.h>
//找到树的重心，并输出删除重心后，剩下的连通区块中最大的结点数
using namespace std;
const int N = 1e5 + 10, M = N * 2;

int h[N], val[M], ne[M], idx;
bool vis[N];
int n;
int ans = N;

void add(int a, int b)
{
	val[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

int DFS(int start)
{
	vis[start] = true;
	int sum = 1;
	int res = 0;
	for (int i = h[start]; i != -1; i = ne[i])
	{
		if (!vis[val[i]])
		{
			int s = DFS(val[i]);
			res = max(s,res);//记录当前结点向下的连通区块中的最大连通区块
			sum += s;//记录包括当前节点在内所有向下的连通区块的结点总数
		}
	}
	res = max(res, n - sum);//判断当前结点向上的连通区块的节点数是否为最大值
	ans = min(ans, res);//所有最大值里挑一个最小值
	return sum;//返回包括当前结点下面的所有连通区块的结点总数
}
int main()
{
	memset(h, -1, sizeof(h));
	scanf("%d", &n);
	for (int i = 1; i < n; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(a, b), add(b, a);
	}
	DFS(1);
	cout << ans << endl;
}
```



# 树与图的BFS（点的层次问题）

```
#include<bits/stdc++.h>
//求从1结点到n结点的最短距离

using namespace std;
const int N = 1e5 + 10;

int h[N], val[N], ne[N], idx;

int d[N], q[N];//记录距离的数组，模拟队列数组

int n, m;

void add(int a, int b)
{
	val[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

int BFS()
{
	int hh = 0, tt = -1;
	q[++tt] = 1;
	memset(d, -1, sizeof(d));
    d[1] = 0;
	while (hh <= tt)
	{
		int t = q[hh++];
		for (int i = h[t]; i != -1; i = ne[i])
		{
			if (d[val[i]] == -1)
			{
				d[val[i]] = d[t] + 1;
				q[++tt] = val[i];
			}
		}
	}

	return d[n];
}
int main()
{
	scanf("%d%d", &n, &m);
	memset(h, -1, sizeof(h));
	for (int i = 0; i < m; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(a, b);
	}
	
	cout << BFS() << endl;
}
```



# 有向图的拓扑序列

```
拓扑序列：若一个由图中所有点构成的序列A满足：对于图中的每条边 (x,y)，x在A中都出现在y之前，则称A是该图的一个拓扑序列。（）。注意是针对图中所有的排序是拓扑排序
//基于BFS实现的拓扑排序
#include<bits/stdc++.h>

using namespace std;
const int N = 1e5 + 10;

int h[N], val[N], ne[N], idx;

int d[N], q[N];//记录入度的数组，模拟队列数组

int n, m;

void add(int a, int b)
{
	val[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

bool topsort()
{
	int hh = 0, tt = -1;

	for (int i = 1; i <= n; i++)
	{
		if (!d[i])q[++tt] = i;
	}//找到所有入度为零的点，并且放入队列

	while (hh <= tt)
	{
		int t = q[hh++];

		for (int i = h[t]; i != -1; i = ne[i])
		{
			d[val[i]]--;//对所有搜素到的点，对他的入度减一，代表删除他的那条入度边
			if (!d[val[i]])//如果入度为零，进入队列
			{
				q[++tt] = val[i];
			}
		}
	}

	return tt == n - 1;//如果队列有n个点代表至少存在一个拓扑排序
}

int main()
{
	scanf("%d%d", &n, &m);
	memset(h, -1, sizeof(h));
	for (int i = 0; i < m; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(a, b);
		d[b]++;
	}
	
	if (topsort())
	{
		for (int i = 0; i < n; i++)
		{
			printf("%d ", q[i]);
		}//队列中的点的插入顺序就是拓扑序列
		puts("");
	}
	else
	{
		printf("-1\n");
	}
}
```



# Dijkstra算法(朴素版)单源不处理负权边

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 510;

int qmap[N][N], dis[N];
bool vis[N];
int n, m;

int dijkstra()
{
	memset(dis,0x3f3f3f3f, sizeof(dis));//初始化距离数组
	dis[1] = 0;

	for (int i = 0; i < n; i++)//我们要把N个点全部标记完，所以需要N次循环
	{
		int t = -1;
		for (int j = 1; j <= n; j++)
		{
			if (!vis[j] && (t == -1 || dis[t] > dis[j]))
			{
				t = j;
			}
		}//路径更新后，寻找当前距离起点最短的点
		vis[t] = true;

		for (int j = 1; j <= n; j++)
		{
			dis[j] = min(dis[j], dis[t] + qmap[t][j]);
		}//更新最短路径
	}

	if (dis[n] != 0x3f3f3f3f)return dis[n];
	else return -1;

}

int main()
{
	scanf("%d%d", &n, &m);
	memset(qmap, 0x3f3f3f3f, sizeof(qmap));//初始化图
	for (int i = 0; i < m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		qmap[a][b] = min(qmap[a][b], c);//重边，所以只取两点之间最短的那条边
	}

	int ans = dijkstra();
	printf("%d\n", ans);
}
```



# Dijkstra算法(堆优化版)单源不处理负权边

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 150010;
typedef pair<int, int> PII;//注意这里，排序规则默认以key值(first元素)

int n, m;
int h[N], w[N], e[N], ne[N], idx;//头节点，权重，结点数组，指针数组，下标
bool vis[N];//标记
int dis[N];//记录距离

void add(int a, int b, int c)
{
	e[idx] = b;
	w[idx] = c;
	ne[idx] = h[a];
	h[a] = idx++;
}

int dijkstra()
{
	memset(dis, 0x3f3f3f3f, sizeof(dis));
	priority_queue<PII, vector<PII>, greater<PII>>heap;
	//优先队列模拟堆，参数意义，队列元素，实现方式，以及是小根堆还是大根堆

	dis[1] = 0;
	heap.push({ 0,1 });//放入初始结点

	while (heap.size())
	{
		auto t = heap.top();//拿出队头元素，即小根堆的顶点，最小值
		heap.pop();

		int ver = t.second, distance = t.first;
		if (vis[ver])continue;//判断队头元素是否被标记过

		vis[ver] = true;
		for (int i = h[ver]; i != -1; i = ne[i])//拿队头元素更新其他结点
		{
			int p = e[i];
			if (dis[p] > distance + w[i])
			{
				dis[p] = distance + w[i];
				heap.push({ dis[p],p });
			}
		}
	}

	if (dis[n] == 0x3f3f3f3f)return -1;
	else return dis[n];
}

int main()
{
	memset(h, -1, sizeof(h));
	scanf("%d%d", &n, &m);
	for (int i = 0; i < m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		add(a, b, c);
	}
	cout << dijkstra() << endl;
}
```



# Bellman-ford求限制边数的最短路单源

```
//给定一个 n 个点 m 条边的有向图，图中可能存在重边和自环， 边权可能为负数。请你求出从 1 号点到 n 号点的最多经过 k 条边的最短距离，如果无法从 1 号点走到 n 号点，输出 impossible。
//注意：图中可能 存在负权回路 。
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 1e5 + 10;

int n, m, k;

struct qxp
{
	int a, b, w;
};

qxp qmap[N];
int dis[N], backup[N];

int bellman_ford()
{
	memset(dis, 0x3f3f3f3f, sizeof(dis));
	dis[1] = 0;
	for (int i = 0; i < k; i++)//连k条边
	{
		memcpy(backup, dis, sizeof(dis));
		for (int j = 0; j < m; j++)
		{
			int a = qmap[j].a, b = qmap[j].b, w = qmap[j].w;
			dis[b] = min(dis[b], backup[a] + w);
		}
	}
	return dis[n];
}



int main()
{
	scanf("%d%d%d", &n, &m, &k);
	for (int i = 0; i < m; i++)scanf("%d%d%d", &qmap[i].a, &qmap[i].b, &qmap[i].w);
	int ans = bellman_ford();
	if (ans >= 0x3f3f3f3f / 2)printf("impossible\n");
	else cout << ans << endl;
	
}
```



# SPFA单源最短路

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 1e5 + 10;

int n, m;
int h[N], e[N], w[N], ne[N], idx;//头结点，结点，权重，指针，下标

int dis[N];//距离数组
bool vis[N];//标记数组，用于记录进入队列的结点，并标记

void add(int a, int b, int c)
{
	e[idx] = b;
	w[idx] = c;
	ne[idx] = h[a];
	h[a] = idx++;
}

int SPFA()
{
	memset(dis, 0x3f3f3f3f, sizeof(dis));//初始化距离数组
	queue<int>q;
	dis[1] = 0;
	q.push(1);
	vis[1] = true;
	while (q.size())
	{
		auto t = q.front();//出队列
		q.pop();
		vis[t] = false;
		for (int i = h[t]; i != -1; i = ne[i])
		{
			int p = e[i];
			if (dis[p] > dis[t] + w[i])//松弛操作
			{
				dis[p] = dis[t] + w[i];
				if (!vis[p])//如果没有入队，则入队
				{
					q.push(p);
					vis[p] = true;//标记已经入队
				}
			}
		}
	}
	return dis[n];
}



int main()
{
	memset(h, -1, sizeof(h));//初始化头节点
	scanf("%d%d", &n, &m);
	for (int i = 0; i < m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		add(a, b, c);
	}
	int ans = SPFA();
	if (ans == 0x3f3f3f3f)printf("impossible\n");
	else printf("%d\n", ans);
	
}
```



# SPFA判断是否存在负环

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 1e5 + 10;

int n, m;
int h[N], e[N], w[N], ne[N], idx;

int dis[N], cnt[N];
bool vis[N];

void add(int a, int b, int c)
{
	e[idx] = b;
	w[idx] = c;
	ne[idx] = h[a];
	h[a] = idx++;
}

bool SPFA()
{
	memset(dis, 0x3f3f3f3f, sizeof(dis));
	queue<int>q;
	for (int i = 1; i <= n; i++)
	{
		q.push(i);
		vis[i] = true;
	}
	//因为判断的是负环，所以不用初始化为零，并且需要将所有点放入队列，来确保不会有环漏掉
	while (q.size())
	{
		auto t = q.front();
		q.pop();
		vis[t] = false;
		for (int i = h[t]; i != -1; i = ne[i])
		{
			int p = e[i];
			if (dis[p] > dis[t] + w[i])//只有当前线段的权重为负数才会进入判断
			{
				dis[p] = dis[t] + w[i];
				cnt[p] = cnt[t] + 1;
				//如果到p点的线段有n条，则说明经过n+1个点，说明有重复点，即环，当且仅当存在负环时才会进入该判定，
				//只要重复次数大于最坏情况n即可判定存在环
				if (cnt[p] >= n) return true;
				if (!vis[p])
				{
					q.push(p);
					vis[p] = true;;
				}
			}
		}
	}
	return false;
}



int main()
{
	memset(h, -1, sizeof(h));
	scanf("%d%d", &n, &m);
	for (int i = 0; i < m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		add(a, b, c);
	}
	if (SPFA())printf("Yes\n");
	else printf("No\n");
}
```



# Floyd多源最短路径（n^3）

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 205;
int n, m, k;

int dis[N][N];

void floyd()
{
	for (int k = 1; k <= n; k++)//先枚举待插入的点
	{
		for (int i = 1; i <= n; i++)//在枚举边
		{
			for (int j = 1; j <= n; j++)
			{
				dis[i][j] = min(dis[i][k] + dis[k][j], dis[i][j]);//更新
			}
		}
	}
}


int main()
{
	scanf("%d%d%d", &n, &m, &k);
	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= n; j++)
		{
			if (i == j)dis[i][j] = 0;
			else dis[i][j] = 0x3f3f3f3f;
		}
	}
	for (int i = 1; i <= m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		dis[a][b] = min(dis[a][b], c);
	}
	floyd();

	while (k--)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		int ans = dis[a][b];
		if (ans > 0x3f3f3f3f/2)printf("impossible\n");
		else printf("%d\n", ans);
	}
}
```



# Prime求最小生成树（较慢）

```
//生成树：一个连通图的生成树是一个极小的连通子图，它包含图中全部的n个顶点，但只有构成一棵树的n-1条边。
//最小生成树：所谓一个 带权图 的最小生成树，就是原图中边的权值最小的生成树 ，所谓最小是指边的权值之和小于或者等于其它生成树的边的权值之和。
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 510, INF = 0x3f3f3f3f;

int n, m;
int qmap[N][N], dis[N];
bool vis[N];

int prim()
{
	memset(dis, INF, sizeof(dis));
	int res = 0;//记录最小生成树的边的权重值
	for (int i = 0; i < n; i++)
	{
		int t = -1;
		for (int j = 1; j <= n; j++)
		{
			if (!vis[j] && (t == -1 || dis[t] > dis[j]))
			{
				t = j;
			}
		}

		if (i && dis[t] == INF)return INF;
		if (i)res += dis[t];

		for (int j = 1; j <= n; j++)
		{
			dis[j] = min(dis[j], qmap[t][j]);//这里更新的是距离标记点集合的最小距离
		}
		vis[t] = true;
	}
	return res;
}

int main()
{
	scanf("%d%d", &n, &m);
	memset(qmap, INF, sizeof(qmap));
	for (int i = 1; i <= m; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		qmap[a][b] = qmap[b][a] = min(qmap[a][b], c);//！！！无向图
	}
	int ans = prim();
	if (ans == INF)printf("impossible\n");
	else printf("%d\n", ans);
}
```



# Kruskal求最小生成树

```
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 2e5+10, INF = 0x3f3f3f3f;

int n, m;
int fa[N];
struct qxp
{
	int a, b, w;
};

qxp qmap[N];

bool cmp(qxp a, qxp b)
{
	return a.w < b.w;
}

void init()//初始化并查集
{
	for (int i = 1; i <= n; i++)
	{
		fa[i] = i;
	}
}

int find(int x)
{
	if (fa[x] != x) fa[x] = find(fa[x]);
	return fa[x];
}//并查集

int Kruskal()
{
	init();
	sort(qmap, qmap + m, cmp);//对所有边按照升序进行排序
	int cnt = 0, res = 0;
	for (int i = 0; i < m; i++)
	{
		int a = qmap[i].a, b = qmap[i].b;
		a = find(a), b = find(b);//查询是否在同一个集合
		if (a != b)
		{
			fa[a] = b;//并入同一个集合
			res += qmap[i].w;//记录权重总和
			cnt++;//记录边数
		}
	}
	if (cnt < n - 1)return INF;//如果所有边都被放入一个集合，则证明存在最小生成树
	else return res;
}
int main()
{
	

	scanf("%d%d", &n, &m);
	for (int i = 0; i < m; i++)
	{
		scanf("%d%d%d", &qmap[i].a, &qmap[i].b, &qmap[i].w);
	}
	
	int ans = Kruskal();
	if (ans == INF)printf("impossible\n");
	else printf("%d\n", ans);
}
```



# 染色法判定二分图

```
二分图：设G=(V,E)是一个无向图，如果顶点V可分割为两个互不相交的子集(A,B)，并且图中的每条边（i，j）所关联的两个顶点i和j分别属于这两个不同的顶点集，则称图G为一个二分图。
一个图如果是二分图，当且仅当，图中不含奇数环(环中边的的数量是奇数)
#include<bits/stdc++.h>
#include<algorithm>
using namespace std;
const int N = 1e5 + 10, M = 2e5 + 10;
int n, m;
int h[N], e[M], ne[M], idx;
int color[N];//染色数组

void add(int a, int b)
{
	e[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}
bool dfs(int start,int c)
{
	color[start] = c;
	for (int i = h[start]; i != -1; i = ne[i])
	{
		if (!color[e[i]])
		{
			if (!dfs(e[i], 3 - c))return false;
		}
		else if(color[e[i]] == c)
		{
			return false;
		}
	}
	return true;
}

int main()
{
	memset(h, -1, sizeof(h));
	scanf("%d%d", &n, &m);
	for (int i = 0; i < m; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(a, b),add(b, a);
	}
	bool ans = true;
	for (int i = 1; i <= n; i++)
	{
		if (!color[i])
		{
			if (!dfs(i, 1))
			{
				ans = false;
				break;
			}
		}
	}
	if (ans)printf("Yes\n");
	else printf("No\n");
}
```



# 匈牙利算法（二分图最大匹配）

```
#include<bits/stdc++.h>
using namespace std;
const int N = 510, M = 1e5 + 10;
int n1, n2, m;
int h[N], e[M], ne[M], idx;
int match[N];
bool vis[N];

void add(int a, int b)
{
	e[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

bool find(int x)
{
	for (int i = h[x]; i != -1; i = ne[i])
	{
		int d = e[i];
		if (!vis[d])
		{
			vis[d] = true;
			if (match[d] == 0 || find(match[d]))//寻找该妹子是否有其他的选择
			{
				match[d] = x;
				return true;
			}
		}
	}
	return false;
}

int main()
{
	memset(h, -1, sizeof(h));
	scanf("%d%d%d", &n1, &n2, &m);
	for (int i = 0; i < m; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(a, b);
	}

	int ans = 0;

	for (int i = 1; i <= n1; i++)
	{
		memset(vis, false, sizeof(vis));//因为下一轮如果该妹子可以被其他男生选中，则需要更新她的标记
		if (find(i))
		{
			ans++;
		}
	}
	printf("%d\n", ans);
}
```



# 分解质因数

```
对于n来说，他的质因子要么等于根号n，要么成对出现在根号n的两侧且必定一大一小，假设有两对质因子从小到大排列是P，Q，(根号n)，S，T，则P*T=Q*S=n，那么P=(Q*S)/T，那么T一定是Q或S约数，一但一个数出现了约数，他就不是质数，所以在所有的质数里不存在两对质数的积等于n，也就是说等于n的质因数对最多有一个，也就最多有一个质因数大于根号n。
唯一分解定理：任何一个大于1的整数n都可以分解成若干个素因数的连乘积
N=p1^a1*p2^a2*...pk^ak

#include<bits/stdc++.h>

using namespace std;
typedef long long ll;
void divide(int a)
{
	for (int i = 2; i <= a / i; i++)//循环次数是sqrt(a)
	{
		if (a % i == 0)
		{
			int res = 0;
			while (a % i == 0)
			{
				res++;
				a /= i;
			}
			cout << i << " " << res << endl;
		}
	}
	if (a > 1)
	{
		cout << a << " " << 1 << endl;
	}
}
int main()
{
	int n;
	scanf("%d", &n);
	while (n--)
	{
		int a;
		scanf("%d", &a);
		divide(a);
		cout<<endl;
	}
}
```



# 埃氏筛

```
const int N = 1e6 + 10;
bool st[N];
int primes[N];//存质数的数组
int cnt = 0;
void get_primes(int a)
{
	for (int i = 2; i < N; i++)
	{
		if (primes[i])
		{
			continue;
		}
		primes[cnt++] = i;
		for (int j = i + i; j < N; j += i)
		{
			st[j] = true;
		}
	}
}
```



# 欧拉筛

```
#include<bits/stdc++.h>

using namespace std;
typedef long long ll;
const int N = 1e6+10;
int n;
bool st[N];
int primes[N];//存质数的数组
int cnt = 0;
void get_primes()
{
	for (int i = 2; i <= n; i++)
	{
		if (!st[i])primes[cnt++] = i;
		for (int j = 0; primes[j] * i <= n; j++)//枚举所有素数，其中待筛的数i*isprimes[j]不能超过数据范围
		{
			st[primes[j] * i] = true;//将该素数作为最小质因数，筛掉它的所有倍数
			if (i % primes[j] == 0)break;
			//i%primes[j]==0则，k*primes[j]=i;则对于primes[j+1]来i*primes[j+1]=k*primes[j]*primes[j+1],
			//则primes[j+1]不能保证为最小质因数
		}
	}
	cout<<cnt<<endl;
}

int main()
{
	cin >> n;
	get_primes();
}
```



# 约数个数

```
一个数约数的个数：分解质因数，求出每个质因数的底数和指数，约数个数就等于每个质因数的（指数+1）求积
对于n来说，n=p1^a1*p2^a2*....*pn^an
假设d是n的任意一个约数，d=p1^b1*p2^b2+...*pn^bn.
那么一定有一对（β1，β2...βk）可以使下式成立。
重点在于每一种b1-bk都代表了一种取法，所有的取法数就等于每个a的数量加1（因为是0-a1）
所以个数为 (a1+1)*(a2+1)*....*(an+1)

#include<bits/stdc++.h>
#include<unordered_map>

using namespace std;
typedef long long ll;
  
const int mod = 1e9 + 7;

int main()
{
	int n;
	cin >> n;
	unordered_map<int, int>prime;
	while (n--)
	{
		int a;
		cin >> a;
		for (int i = 2; i <= a / i; i++)
		{
			while (a % i == 0)
			{
				a /= i;
				prime[i] += 1;;
			}
		}
		if (a > 1)prime[a]++;
	}

	ll res = 1;
	for (auto it : prime)
	{
		res *= (it.second + 1);
		res %= mod;
	}
	cout << res << endl;
}
```



# 约数之和

```
总和：(p1^0+p1^1+...p1^a1)*...(pk^0+pk^2+...pk^ak)
每一个相乘的结果代表一个约数

#include <iostream>
#include <algorithm>
#include <unordered_map>
#include <vector>

using namespace std;

typedef long long LL;

const int N = 110, mod = 1e9 + 7;

int main()
{
    int n;
    cin >> n;

    unordered_map<int, int> primes;

    while (n -- )
    {
        int x;
        cin >> x;

        for (int i = 2; i <= x / i; i ++ )
            while (x % i == 0)
            {
                x /= i;
                primes[i] ++ ;
            }

        if (x > 1) primes[x] ++ ;
    }

    LL res = 1;
    for (auto p : primes)
    {
        LL a = p.first, b = p.second;
        LL t = 1;
        while (b -- ) t = (t * a + 1) % mod;
        res = res * t % mod;
    }

    cout << res << endl;

    return 0;
}
```



# 最大公约数和最小公倍数（欧几里得算法）

```
int gcd(int a, int b)
{
    return b ? gcd(b, a % b) : a;
}//最大公约数

int lcm(int a, int b)
{
	int g = gcd(a, b);
	return (a / g) * (b / g) * g;
}//最小公倍数

```



# 欧拉函数

```
1~n中与n互质的数的个数称为欧拉函数，记作f(n).
若在算数基本定理中，n=p1^a1+p2^a2+...pm^am,
则f(n)=n*((p1-1)/p1)*((p2-1)/p2)*..*((pm-1)/pm)
互质：两个数没有除1以为的公约数

#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
typedef long long ll;
int main()
{
	int n;
	cin >> n;
	while (n--)
	{
		int a;
		scanf("%d", &a);
		int res = a;
		for (int i = 2; i <= a / i; i++)
		{
			if (a % i == 0)
			{
				res = res / i * (i - 1);
				while (a % i == 0)a /= i;
			}
		}
		if (a > 1)res = res / a * (a - 1);
		printf("%d\n", res);
	}
}

```



# 欧拉筛求欧拉函数

```
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
typedef long long ll;

const int N = 1e6 + 10;
int primes[N], phi[N];//质数表，欧拉函数数组
bool st[N];

int n, cnt;

void get_erulers()
{
	phi[1] = 1;
	for (int i = 2; i <= n; i++)
	{
		if (!st[i])
		{
			primes[cnt++] = i;
			phi[i] = i - 1;//如果数字n为素数，则他的欧拉函数等于n-1
		}

		for (int j = 0; primes[j] <= n / i; j++)
		{
			//以下分两种情况讨论，分别是,i%primes[j]==和i%primes[j]!=0
			st[primes[j] * i] = true;//筛数
			if (i % primes[j] == 0)
			{
				phi[i*primes[j]] = primes[j] * phi[i];
				//对于欧拉函数f(n)而言
				//对于f(i)而言,因为i%primes[j]==0,则说明primes[j]为i的一个质因数
				//，则f(i)=i*((p1-1)/p1)*((p2-1)/p2)*..*((pm-1)/pm)中的某个p就是primes[j]
				//对于f(i*primes[j])从唯一分解定理的角度来说，
				//i*primes[j]的质因数跟i一样，所以f(i*primes[j])=primes[j]*f(i)
				break;
			}
			phi[i*primes[j]] = phi[i] * (primes[j] - 1);
			//同理对于这种情况而言，primes[j]不是i的质因数，但一定是i*primes[j]的质因数
			//对于i*primes[j]而言，它只比i多了一个质因数primes[j],
			//f(i*primes[j])=primes[j]*f(i)*(1-1/primes[j])
			//化解后就等于,f(i*primes[j])=f(i)*(priems[j]-1)
		}
	}

	ll res = 0;
	for (int i = 1; i <= n; i++)
	{
		res += phi[i];
	}
	cout << res << endl;
}

int main()
{
	cin >> n;
	get_erulers();
}
```



# 快速幂

```
typedef long long ll;

ll quick_pow(int a, int k, int p)
{
	ll res = 1;
	while (k)
	{
		if (k & 1)res = res * a % p;
		a = a * ll(a) % p;
		k >>= 1;
	}
	return res;
}
```

# 矩阵快速幂

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 3;

int n, m;

void mul(int c[], int a[], int b[][N])
{
	int temp[N] = { 0 };
	for (int i = 0; i < N; i++)
	{
		for (int j = 0; j < N; j++)
		{
			temp[i] = (temp[i] + (ll)a[j] * b[j][i]) % m;
		}
	}
	memcpy(c, temp, sizeof(temp));
}

void mul(int c[][N], int a[][N], int b[][N])
{
	int temp[N][N] = { 0 };

	for (int i = 0; i < N; i++)
	{
		for (int j = 0; j < N; j++)
		{
			for (int k = 0; k < N; k++)
			{
				temp[i][j] = (temp[i][j] + (ll)a[i][k] * b[k][j]) % m;
			}
		}
	}

	memcpy(c, temp, sizeof(temp));
}

int main()
{
	ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

	cin >> n >> m;

	int f1[N] = { 1,1,1 };
	int a[N][N] = {
		{0, 1, 0},
		{1, 1, 1},
		{0, 0, 1}
	};

	n--;

	while (n)
	{
		if (n & 1)mul(f1, f1, a);
		mul(a, a, a);
		n >>= 1;
	}

	cout << f1[2] << "\n";
}
```



# 快速幂求除法逆元

```

//乘法逆元的定义：若整数b,m互质，并且对于任意的整数a，如果满足b整除a，则存在一个整数x，使得(a/b)%m==(a*x)%m,则称x为b的模m乘法逆元.
//当 b与m互质的时候，且模数m为质数时， b的乘法逆元为 b^(m-2)。
//当 b是m的倍数时，b的逆元不存在。




#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

ll quick_pow(int a, int k, int p)
{
	ll res = 1;
	while (k)
	{
		if (k & 1)res = res * a % p;
		a = a * ll(a) % p;
		k >>= 1;
	}
	return res;
}


int main()
{
	int n;
	scanf("%d", &n);
	while (n--)
	{
		int a, p;
		scanf("%d%d", &a, &p);
		int res = quick_pow(a, p - 2, p);
		if (a % p != 0)printf("%d\n", res);
		else printf("impossible\n");
	}
}
```



# 扩展欧几里得算法

```
裴蜀定理：对于任意一对整数a,b，一定存在一对整数x,y，使得ax+by=gcd(a,b)，这个公约数是他们能凑出来的最小的正整数，且ax+by凑出来的所有数都是a,b的最大公约数的倍数//gcd(a,b)是a和b的最大公约数

//本题的含义是找到一组ax+by=gcd(a,b)的解并输出


#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int x, y;
int exgcd(int a, int b, int &x, int &y)
{
	if (b == 0)
	{
		x = 1;
		y = 0;
		return a;
	}
	int d = exgcd(b, a % b, y, x);
	//b对应的系数为y，当b被交换时，系数也要被交换
	//b*y+(a%b)*x=d,b*y+(a-[a/b]*b)*x=d,a*x+b*(y-[a/b]*x)
	//通过最大公约数对两轮状态建立方程，寻找转化关系
	y -= a / b * x;
	return d;
}


int main()
{
	int n;
	scanf("%d", &n);
	while (n--)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		exgcd(a,b,x,y);
		printf("%d %d\n", x, y);
	}
}
```



# 线性同余方程



```
对于方程(a*x)%m=b%m,求解x的值
题目分析：(a*x)%m=b%m,a*x=m*y+b,如果b是a和m的最大公约数的倍数，则可以使用扩展欧几里得算法求解方程，最后将解扩大到b/gcd(a,b)倍等于依旧成立，所以扩大后的解就是我们要的解
注：扩展欧几里得可以求模数不是质数的逆元，可以转化为线性同余方程进行求解

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int x, y;
int exgcd(int a, int b, int &x, int &y)
{
	if (b == 0)
	{
		x = 1;
		y = 0;
		return a;
	}
	int d = exgcd(b, a % b, y, x);
	y -= a / b * x;
	return d;
}


int main()
{
	int n;
	scanf("%d", &n);
	while (n--)
	{
		int a, b, m;
		scanf("%d%d%d", &a, &b, &m);
		int d = exgcd(a, m, x, y);
		if (b % d)puts("impossible");
		else printf("%d\n", ll(x) * (b / d) % m);
		//ax+my=b⇔a(km+r)+my=b⇔ar+m(y+ak)=b  r=x%m 所以令x=x%m,y=y+ak等式依旧成立
		//mod m可以卡死答案的数据范围
	}
}

```



# 中国剩余定理

```
m1,m2,...mk互质
对于方程
{
     x%m1=a1%m1
     x%m2=a2%m2
     ........
     x%mk=ak%mk
}
M=m1*m2*...mk，Mi=M/mi,Mi^-1是Mi%mi的逆元
则该方程组的解为x=a1*M1*M1^-1+a2*M2*M2^-1+...ak*Mk*Mk^-1
对于方程组中任意一个方程x%mi=ai%mi来说，解的第i项
Mi*Mi^-1=1,又因为其他项都是mi的倍数，所以%mi为0，将解带入刚好等于ai


```



# 扩展中国剩余定理

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
//题意，给定n个方程，形如x%mi=a%mi,求解这一方程组

ll exgcd(ll a, ll b, ll &x, ll &y)
{
	if (b == 0)
	{
		x = 1;
		y = 0;
		return a;
	}
	ll d = exgcd(b, a % b, y, x);
	y -= a / b * x;
	return d;
}


int main()
{
	int n;
	scanf("%d", &n);
	ll m1, a1;
	scanf("%lld%lld", &m1, &a1);
	n--;
	bool ans = true;//记录是否出现无解的情况
	while (n--)
	{
		ll m2, a2;
		scanf("%lld%lld", &m2, &a2);
		//单看两个方程
		//x%m1=a%m1
		//x%m2=a%m2
		//我们进行一个变形 
		//x=m1*k1+a1
		//x=m2*k2+a2
		//合并方程得k1*m1-k2*m2=a2-a1
		//观察可以发现，该方程形如ax+my=b,可以使用扩展欧几里得算法进行求解，此时k1,k2就是x,y，b就是m2-m1, a,m分别是a1和a2
		ll k1, k2;
		ll d = exgcd(m1, m2, k1, k2);
		//如果b不是d的倍数，则无解
		if ((a2 - a1) % d)
		{
			ans = false;
		}
		//此时k1,k2还只是当m2-m1为gcd(a1,a2)下的值，我们需要将它扩大到m2-m1下的值
		k1 *= (a2 - a1) / d;
		//此时根据定理,方程的通解为k1+(m2/gcd(a1,a2))
		//将求得的值代回方程，x=m1*(k1+(m2/gcd(m1,m2))+a1,x=k1m1+a1+k1*m1*(m2/gcd(m1,m2))
		//将k1*m1+a1当作a k*(m1*m2/gcd(m1,m2))当作k*m，由此我们合并了两个方程，重复这个操作便可以求出解
		ll t = m2 / d;
		k1 = (k1 % t + t) % t;
		//取模，+t是负数取模,因为m2-m1可能为负数
		//k1的值到下一轮循环再次变成未知变量
		a1 = k1 * m1 + a1;
		m1 = m1 / d * m2;
	}
	if (!ans)printf("-1\n");
	else
	{
		ll x = (a1 % m1 + m1) % m1;
		printf("%lld\n", x);
	}
}
```



# 高斯消元求解线性方程组

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 110;
const double ops = 1e-8;
double a[N][N];
int n;

int gaoss()
{
	int c, r;//列，行
	for (c = 0, r = 0; c < n; c++)
	{
		int t = r;
		for (int i = r; i < n; i++)
		{
			if (abs(a[i][c]) > abs(a[t][c]))
			{
				t = i;
			}
		}//枚举行数，找到当前这一列中最大的那一行
		
		if (abs(a[t][c]) < ops)
		{
			continue;
		}//当前列不存在非零系数

		for (int i = c; i <= n; i++)
		{
			swap(a[r][i], a[t][i]);
		}//将选中的那一行放到未处理行里的最上面

		for (int i = n; i >= c; i--)
		{
			a[r][i] /= a[r][c];
		}//将选中行的第一列变成1

		for (int i = r + 1; i < n; i++)
		{
			if (abs(a[i][c]) > ops)//如果当前这一行的未处理的首元素不为零
			{
				for (int j = n ; j >= c; j--)
				{
					a[i][j] -= a[i][c] * a[r][j];//该行的未处理的首元素*该列对应到目标行数的元素
				}
			}
		}//将待选行的未处理首相消为0
		r++;
	}

	if (r < n)
	{
		for (int i = r; i < n; i++)
		{
			if (abs(a[i][n]) > ops)
			{
				return 0;//无解
			}
		}
		return 2;//无穷多解
	}

	for (int i = n - 1; i >= 0; i--)
	{
		for (int j = i + 1; j < n; j++)
		{
			a[i][n] -= a[i][j] * a[j][n];
		}
	}
	return 1;//唯一解
}

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n+1; j++)
		{
			cin >> a[i][j];
		}
	}
	int ans = gaoss();
	if (ans == 2)puts("Infinite group solutions");
	else if (ans == 0)puts("No solution");
	else
	{
		for (int i = 0; i < n; i++)
		{
			printf("%.2lf\n", a[i][n]);
		}
	}
}
```



# 高斯消元求解异或线性方程组

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 110;
int a[N][N];
int n;

int gaoss()
{
	int r, c;
	for (c = 0, r = 0; c < n; c++)
	{
		int t = r;
		for (int i = r; i < n; i++)
		{
			if (a[i][c])
			{
				t = i;
				break;
			}
		}

		if (!a[t][c])continue;

		for (int i = c; i <= n; i++)swap(a[t][i], a[r][i]);

		for (int i = r + 1; i < n; i++)
		{
			if (a[i][c])
			{
				for (int j = n; j >= c; j--)
				{
					a[i][j] ^= a[r][j];
				}
			}
		}

		r++;
	}

	if (r < n)
	{
		for (int i = r; i < n; i++)
		{
			if (a[i][n])
			{
				return 0;
			}
		}
		return 2;
	}

	for (int i = n - 1; i >= 0; i--)
	{
		for (int j = i + 1; j < n; j++)
		{
			a[i][n] ^= (a[j][n] * a[i][j]);
		}
	}
		
	return 1;
}

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n+1; j++)
		{
			cin >> a[i][j];
		}
	}
	int ans = gaoss();
	if (ans == 2)puts("Multiple sets of solutions");
	else if (ans == 0)puts("No solution");
	else
	{
		for (int i = 0; i < n; i++)
		{
			printf("%d\n", a[i][n]);
		}
	}
}
```



# 求组合数(利用递推式预处理组合数数组)

```
//C(a,b)=c(a-1,b)+c(a-1,b-1)

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int mod = 1e9 + 7;
const int N = 2010;//a,b的数据范围
int c[N][N];//组合数预处理数组

void init()
{
	for (int i = 0; i < N; i++)
	{
		for (int j = 0; j <= i; j++)
		{
			if (!j)c[i][j] = 1;
			else c[i][j] = (c[i - 1][j] + c[i - 1][j - 1]) % mod;
		}
	}
}

int main()
{
    init();
	int n;//10000以内的数据范围
	scanf("%d", &n);
	while (n--)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		printf("%d\n", c[a][b]);
	}
}
```



# 求组合数（预处理阶乘数组和阶乘逆元数组）

```
//C(a,b)=a!/(b!*(a-b)!)

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int mod = 1e9 + 7;
const int N = 1e5 + 3;//a,b的数据范围

int fac[N], infac[N];//阶乘数组和阶乘逆元数组

int quick_pow(int a, int k)
{
	int res = 1;
	while (k)
	{
		if (k & 1)res = (ll)res * a % mod;
		a = (ll)a * a % mod;
		k >>= 1;
	}
	return res;
}

void init()
{
	fac[0] = infac[0] = 1;
	for (int i = 1; i < N; i++)
	{
		fac[i] = (ll)fac[i - 1] * i % mod;
		infac[i] =(ll)infac[i - 1] * quick_pow(i, mod - 2) % mod;
	}
}

int main()
{
	init();
	int n;
	scanf("%d", &n);
	while (n--)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		printf("%d\n", (ll)fac[a] * infac[b] % mod * infac[a - b] % mod);
	}
}
```



# 求组合数（卢卡斯定理）

```
//C(a,b)%p=c(a%p,b%p)*c(a/p,b/p)%p

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int p;//模数

int quick_pow(ll a, ll k)
{
	int res = 1;
	while (k)
	{
		if (k & 1)res = (ll)res * a % p;
		a = (ll)a * a % p;
		k >>= 1;
	}
	return res;
}

int C(ll a, ll b)
{
	int res = 1;
	for (int i = 1, j = a; i <= b; i++, j--)
	{
		res = (ll)res * j % p;
		res = (ll)res * quick_pow(i, p - 2) % p;
	}
	return res;
}

int lucas(ll a, ll b)
{
	if (a < p && b < p)return C(a, b);
	return (ll)C(a % p, b % p) * lucas(a / p, b / p) % p;
}

int main()
{
	int n;
	scanf("%d", &n);
	while (n--)
	{
		ll a, b;
		scanf("%lld%lld%d", &a, &b, &p);
		printf("%d\n", lucas(a, b));
	}
}
```



# 求组合数（不取模高精度计算版本）

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 5005;
int cnt;//记录质数的个数
int primes[N], sum[N];//素数存储数组，第i个素数在待计算的组合数中的出现个数
bool st[N];

void get_primes(int n)
{
	for (int i = 2; i <= n; i++)
	{
		if (!st[i])primes[cnt++] = i;
		for (int j = 0; primes[j] <= n / i; j++)
		{
			st[primes[j] * i] = true;
			if (i % primes[j] == 0)break;
		}
	}
}//筛出a范围内的质数

//a!所含的p的倍数的个数等于a/p+a/p^2+....
int get_cnt(int n, int p)
{
	int res = 0;
	while (n)
	{
		res += n / p;
		n /= p;
	}
	return res;
}

vector<int> mul(vector<int> a, int b)
{
	vector<int>res;
	int t = 0;
	for (int i = 0; i < a.size(); i++)
	{
		t += a[i] * b;
		res.push_back(t % 10);
		t /= 10;
	}

	while (t)
	{
		res.push_back(t % 10);
		t /= 10;
	}
	return res;
}//高精度乘法

int main()
{
	int a, b;
	scanf("%d%d", &a, &b);

	get_primes(a);//找到所有质数

    //根据唯一分解定理，所有的数都可以分解为若干个素数的次数的幂的相乘
    //我们只需要计算组合数里每个素数的个数有多少，再将对应素数的个数的幂乘起来即可
	for (int i = 0; i < cnt; i++)
	{
		int p = primes[i];
		sum[i] = get_cnt(a, p) - get_cnt(b, p) - get_cnt(a - b, p);
	}

	vector<int>res;
	res.push_back(1);
	for (int i = 0; i < cnt; i++)
	{
		for (int j = 0; j < sum[i]; j++)
		{
			res = mul(res, primes[i]);
		}
	}

	for (int i = res.size() - 1; i >= 0; i--)
	{
		printf("%d", res[i]);
	}
}
```



# 卡特兰数（满足条件的01序列）

```
//C(2*n,n)-C(2*n,n-1)=c(2*n,n)/(n+1)

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int mod = 1e9 + 7;
const int N = 1e5 + 3;
int fac[N], infac[N];

int quick_pow(int a,int k)
{
	int res = 1;
	while (k)
	{
		if (k & 1)res = (ll)res * a % mod;
		a = (ll)a * a % mod;
		k >>= 1;
	}
	return res;
}

int C(ll a, ll b)
{
	int res = 1;
	for (int i = 1, j = a; i <= b; i++, j--)
	{
		res = (ll)res * j % mod;
		res = (ll)res * quick_pow(i, mod - 2) % mod;
	}
	return res;
}

int main()
{
	int n;
	scanf("%d", &n);
	int a = 2 * n, b = n;
	int ans = (ll)C(a, b) * quick_pow(n + 1, mod - 2) % mod;
	printf("%d\n", ans);
}

```



# 容斥原理（二进制枚举应用）

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 20;

int p[N];


int main()
{
	int n, m;
	scanf("%d%d", &n, &m);

	for (int i = 0; i < m; i++)
	{
		scanf("%d", &p[i]);
	}
	int res = 0;
	for (int i = 1; i < 1 << m; i++)
	{
		int t = 1, cnt = 0;
		for (int j = 0; j < m; j++)
		{
			if (i >> j & 1)
			{
				cnt++;
				if ((ll)t * p[j] > n)
				{
					t = -1;
					break;
				}
				t *= p[j];
			}
		}
		if (t != -1)
		{
			if (cnt % 2)res += n / t;
			else res -= n / t;
		}
	}//二进制枚举素数的选择情况

	printf("%d\n", res);
}
```



# 博弈论（Nim游戏）

```
//给定 n 堆石子，两位玩家轮流操作，每次操作可以从任意一堆石子中拿走任意数量的石子（可以拿完，但不能不拿），最后无法进行操作的人视为失败。
//问如果两人都采用最优策略，先手是否必胜。

//核心就是每一轮你的选择结束后，要让对方有两个选择
//等价到异或问题，最后剩下的值当作每轮拿的值，按照这个值去拿你必赢，如果对手没有按照这个值去拿，你可以把这个必败状态留给对手
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int main()
{
	int n;
	scanf("%d", &n);
	int res = 0;
	while (n--)
	{
		int a;
		scanf("%d", &a);
		res ^= a;
	}
	if (res)puts("Yes");
	else puts("No");
}
```



# 博弈论（台阶 Nim游戏）

```
现在，有一个 n 级台阶的楼梯，每级台阶上都有若干个石子，其中第 i 级台阶上有 ai 个石子(i≥1)。

两位玩家轮流操作，每次操作可以从任意一级台阶上拿若干个石子放到下一级台阶中（不能不拿）。

已经拿到地面上的石子不能再拿，最后无法进行操作的人视为失败。

问如果两人都采用最优策略，先手是否必胜。

//如果只有偶数上的台阶，你必败，但是只要你奇数台阶还有数量就有赢的可能，现在问题转化为奇数台阶谁先没得拿的问题，

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int main()
{
	int n;
	scanf("%d", &n);
	int res = 0;
	for (int i = 1; i <= n; i++)
	{
		int a;
		scanf("%d", &a);
		if (i & 1)res ^= a;
	}
	if (res)puts("Yes");
	else puts("No");
}
```



# 博弈论（集合，Nim游戏，SG函数）

```
给定 n 堆石子以及一个由 k 个不同正整数构成的数字集合 S。

现在有两位玩家轮流操作，每次操作可以从任意一堆石子中拿取石子，每次拿取的石子数量必须包含于集合 S
，最后无法进行操作的人视为失败。

问如果两人都采用最优策略，先手是否必胜。



Mex运算：设S为一个非负整数集合，求出不属于这个集合的最小的非负整数的运算
SG函数：在有向图游戏中，对于每个结点x，设从x 出发有k条边，定义SG(x)的后继节点y1,y2,...yk
则SG(x)=mex(SG(y1),SG(y2),....SG(yk)),特别的整个有向图游戏G的SG数值等于起点S的数值，记作SG(G)=SG(S)
通过判断重点SG值是否为零来判断是否胜利，如果有多个有向图，解=就将所有有向图的SG值异或起来判断值是否为零
#include <bits/stdc++.h>
#include<unordered_set>
using namespace std;
typedef long long ll;
const int N = 105, M = 1e5 + 8;
int k;
int s[N], f[M];//集合数组，SG数组
int sg(int x)
{
	if (f[x] != -1)return f[x];

	unordered_set<int>S;
	for (int i = 0; i < k; i++)
	{
		if (x >= s[i])S.insert(sg(x - s[i]));
	}
	for (int i = 0;; i++)
	{
		if (!S.count(i))return f[x] = i;
	}
}
int main()
{
	
	scanf("%d", &k);
	for (int i = 0; i < k; i++)
	{
		scanf("%d", &s[i]);
	}

	memset(f, -1,sizeof(f));
	int n;
	scanf("%d", &n);
	int res = 0;
	while (n--)
	{
		int x;
		scanf("%d", &x);
		res ^= sg(x);
	}

	if (res)puts("Yes");
	else puts("No");
}
```



# 博弈论（拆分-Nim游戏）

```
#include <bits/stdc++.h>
#include<unordered_set>
using namespace std;
typedef long long ll;
const int N = 105;
int f[N];//集合数组，SG数组
int sg(int x)
{
	if (f[x] != -1)return f[x];

	unordered_set<int>S;
	for (int i = 0; i < x; i++)
	{
		for (int j = 0; j <= i; j++)
		{
			S.insert(sg(i) ^ sg(j));
		}
	}

	for (int i = 0;; i++)
	{
		if (!S.count(i)) return f[x] = i;
	}
}
int main()
{
	memset(f, -1, sizeof(f));
	int n;
	scanf("%d", &n);
	int res = 0;
	while (n--)
	{
		int x;
		scanf("%d", &x);
		res ^= sg(x);
	}
	if (res)puts("Yes");
	else puts("No");
}

```



# 动态规划（01背包问题）

```


#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

const int N = 1003;
int v[N], w[N];
int dp[N][N];//只从前i个物品里选择，且容积为j时物品价值的最大值

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d%d", &v[i], &w[i]);
	}

	for (int i = 1; i <= n; i++)//枚举物品
	{
		for (int j = 0; j <= V; j++)//枚举体积的所有可能情况
		{
			dp[i][j] = dp[i - 1][j];
			if (j >= v[i])dp[i][j] = max(dp[i][j], dp[i - 1][j - v[i]] + w[i]);
		}
	}
	printf("%d\n", dp[n][V]);
}//朴素版

#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

const int N = 1003;
int v[N], w[N];
int dp[N];//只从前i个物品里选择，且容积为j时物品价值的最大值

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d%d", &v[i], &w[i]);
	}

	for (int i = 1; i <= n; i++)//枚举物品
	{
		for (int j = V; j >= v[i]; j--)//枚举体积的所有可能情况
		{
			//因为j要比v[i]大，所以直接从v[i]开始枚举，又因为j-v[i]比j小，也就是说在循环直接就已经被更新，此时相当于dp[i][j-v[i]]的值
			//因此我们要从大到小枚举
			dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
		}
	}
	printf("%d\n", dp[V]);
}
```



# 动态规划（二维01背包问题）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int K = 103;
const int M = 503;
const int N = 1003;
int c[N], d[N], dp[N][M];

int main()
{
	int n, m, k;
	scanf("%d%d%d", &n, &m, &k);
	for (int i = 1; i <= k; i++)
	{
		scanf("%d%d", &c[i], &d[i]);
		for (int j = n; j >= c[i]; j--)
		{
			for (int p = m - 1; p >= d[i]; p--)//当体力值为0时，不能收复怪物，所以消耗体力不能为m
			{
				dp[j][p] = max(dp[j][p], dp[j - c[i]][p - d[i]] + 1);
			}
		}
	}

	int ans1 = dp[n][m - 1];
	int ans2 = m - 1;
	while (ans2 > 0 && dp[n][ans2 - 1] == dp[n][m - 1])ans2--;
	printf("%d %d\n", ans1, m - ans2);
}
```



# 动态规划（01背包计算刚好满足体积条件的方案数的问题）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 103;
const int M = 10003;
int n, m, a[N], dp[N][M];


int main()
{
	scanf("%d%d", &n, &m);

	for (int i = 1; i <= n; i++) {
		scanf("%d", &a[i]);
		if (a[i] <= m)dp[i][a[i]] = 1;
	}

	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= m; j++)
		{
			dp[i][j] += dp[i - 1][j];
			if (j >= a[i])dp[i][j] += dp[i - 1][j - a[i]];
		}
	}

	printf("%d\n", dp[n][m]);
}

//一维优化版
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 103;
const int M = 10003;
int n, m, a[N], dp[M];


int main()
{
	scanf("%d%d", &n, &m);

	for (int i = 1; i <= n; i++) {
		scanf("%d", &a[i]);
	}
	dp[0] = 1;
	for (int i = 1; i <= n; i++)
	{
		for (int j = m; j >= a[i]; j--)
		{
			dp[j] += dp[j - a[i]];
		}
	}

	printf("%d\n", dp[m]);
}
```

# 动态规划(01背包bitset优化)

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 5e5 + 5;
int a[N];
bitset<N>bt;

int main()
{
    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);
    int n;
    cin >> n;
    int x;
    bt[0] = true;
    for (int i = 0; i < n; i++) {
        cin >> x;
        bt |= (bt << x);
    }

    cout << bt.count() << '\n';
}
//https://cdn.oj.eriktse.com/problem.php?id=1054
```



# 动态规划数论综合

```
题意: 有一个具有n个数的集合，如果存在一个集合两个集合所能表示的数是一样的，则两个集合等价，求使得n最小的等价集合
分析：1: a1 a2 ...an一定可以被标识出来
2：最优解一定从a1 a2..a2中去挑选
3：b1,b2,..bm一定不能被其他bi表示出来
综合以上分析，可得知，我们现在要研究有没有ai可以被集合的中的其他数表示出来，即选不同的数。每个数的数量不限，求装满ai这个的方案数，如果为零代表是最优解的元素

#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 103, M = 25003;
int a[N], dp[M];


void work()
{
	memset(dp, 0, sizeof(dp));
	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++)scanf("%d", &a[i]);

	sort(a, a + n);
	int ans = 0;
	dp[0] = 1;
	for (int i = 0; i < n; i++)
	{
		if (!dp[a[i]])ans++;
		for (int j = a[i]; j <= a[n - 1]; j++)
		{
			dp[j] += dp[j - a[i]];
		}
	}
	
	printf("%d\n", ans);
}

int main()
{
	int T;
	scanf("%d", &T);
	while(T--)
	{
		work();
	}
}

```



# 动态规划（完全背包问题）

```
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

const int N = 1003;
int v[N], w[N];
int dp[N][N];//只从前i个物品里选择，且容积为j时物品价值的最大值

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d%d", &v[i], &w[i]);
	}

	for (int i = 1; i <= n; i++)//枚举物品
	{
		for (int j = 0; j <= V; j++)//枚举体积的所有可能情况
		{
			dp[i][j] = dp[i - 1][j];
			if (j >= v[i])dp[i][j] = max(dp[i][j], dp[i][j - v[i]] + w[i]);
		}
	}
	printf("%d\n", dp[n][V]);
}//可以选无限次某个物品，朴素版


#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

const int N = 1003;
int v[N], w[N];
int dp[N];//只从前i个物品里选择，且容积为j时物品价值的最大值

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d%d", &v[i], &w[i]);
	}

	for (int i = 1; i <= n; i++)//枚举物品
	{
		for (int j = v[i]; j <= V; j++)//枚举体积的所有可能情况
		{
			//因为j要比v[i]大，所以直接从v[i]开始枚举，又因为j-v[i]比j小，也就是说在循环直接就已经被更新，此时相当于dp[i][j-v[i]]的值
			//因此我们要从大到小枚举
			dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
		}
	}
	printf("%d\n", dp[V]);
}
```



# 动态规划（完全背包问题计算方案数）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 1003;
int v, dp[N];


int main()
{
	scanf("%d", &v);
	int a[5] = { 0,10,20,50,100 };
	dp[0] = 1;
	for (int i = 1; i <= 4; i++)
	{
		for (int j = a[i]; j <= v; j++)
		{
			dp[j] += dp[j - a[i]];
		}
	}
	printf("%d\n", dp[v]);
}
```



# 动态规划（多重背包）

```
#include <bits/stdc++.h>

using namespace std;
typedef long long ll;

const int N = 103;
int v[N], w[N], s[N];
int dp[N][N];//只从前i个物品里选择，且容积为j时物品价值的最大值

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d%d%d", &v[i], &w[i], &s[i]);
	}

	for (int i = 1; i <= n; i++)//枚举物品
	{
		for (int j = 0; j <= V; j++)//枚举体积的所有可能情况
		{
			for (int k = 0; k <= s[i] && j - k * v[i] >= 0; k++)
			{
				dp[i][j] = max(dp[i - 1][j - k * v[i]] + w[i] * k, dp[i][j]);
			}
			
		}
	}
	printf("%d\n", dp[n][V]);
}
//每种物品选择数量的限制
```



# 动态规划（多重背包二进制优化）

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 20005, M = 2005;
int v[N], w[N], dp[M];

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	int cnt = 0;
	while (n--)
	{
		int v1, w1, s;
		scanf("%d%d%d", &v1, &w1, &s);
		int k = 1;
		while (k <= s)
		{
			cnt++;
			v[cnt] = k * v1;
			w[cnt] = k * w1;
			s -= k;
			k *= 2;
		}//快速幂思想，来枚举k以内的所有数字情况
		//相当于把这个数拆解为多个二进制整数和一个十进制整数，每一种数字选法，代表挑选了哪些二进制整数
		if (s)
		{
			cnt++;
			v[cnt] = s * v1;
			w[cnt] = s * w1;
		}
	}
	for (int i = 1; i <= cnt; i++)//转化为01背包问题
	{
		for (int j = V; j >= v[i]; j--)
		{
			dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
		}
	}
	printf("%d\n", dp[V]);
}
```

# 多重背包问题（单调队列优化）

```
分析：dp[i][j]=max(dp[i-1][j],dp[i-1][j-v]+w,dp[i-1][j-2*v]+2*w,.....dp[i-1][j-kv]+k*w)
     dp[i][j-v]=max(        ,dp[i-1][j-v]  ,dp[i-1][j-2*v]+  w,.....dp[i-1][j-kv]+(k-1)w,dp[i-1][j-(k+1)v]+kw)
     
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 20003;
int dp[N], c[N], q[N];
int n, m;



int main()
{
	
	scanf("%d%d", &n, &m);

	for (int i = 0; i < n; i++)
	{
		int v, w, s;
		scanf("%d%d%d", &v, &w, &s);
		memcpy(c, dp, sizeof(c));
		for (int j = 0; j < v; j++)
		{
			int hh = 0, tt = -1;
			for (int k = j; k <= m; k += v)
			{
				if (hh <= tt && q[hh] < k - s * v)hh++;
				while (hh <= tt && c[q[tt]] - q[tt] / v * w <= c[k] - k / v * w)tt--;
				q[++tt] = k;
				dp[k] = max(dp[k], c[q[hh]] + (k - q[hh]) / v * w);
			}
		}
	}

	printf("%d\n", dp[m]);

}
```



# 动态规划（分组背包）

```
#include <bits/stdc++.h>//n个箱子，箱子里若干物品，从中任选一个，只能选一次，求最大值
using namespace std;
typedef long long ll;
const int N = 105;
int v[N][N], w[N][N], s[N], dp[N];

int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &s[i]);
		for (int j = 0; j < s[i]; j++)
		{
			scanf("%d%d", &v[i][j], &w[i][j]);
		}
	}

	for (int i = 0; i < n; i++)
	{
		for (int j = V; j >= 0; j--)
		{
			for (int k = 0; k < s[i]; k++)
			{
				if (j >= v[i][k])
				{
					dp[j] = max(dp[j], dp[j - v[i][k]] + w[i][k]);
				}
			}
		}
	}
	printf("%d\n", dp[V]);
}
```



# 动态规划（体积最少为v时的情况）

```
#include<bits/stdc++.h>
using namespace std;

const int N = 1003, M = 100;
int dp[M][M];




int main()
{
	memset(dp, 0x3f, sizeof(dp));
	dp[0][0] = 0;
	int m, n, k;
	scanf("%d%d%d", &m, &n, &k);
	for (int i = 0; i < k; i++)
	{
		int a, b, c;
		scanf("%d%d%d", &a, &b, &c);
		for (int j = m; j >= 0; j--)
		{
			for (int u = n; u >= 0; u--)
			{
				dp[j][u] = min(dp[j][u], dp[max(0, j - a)][max(0, u - b)] + c);
			}
		}
	}

	printf("%d\n", dp[m][n]);
}
```



# 动态规划（求方案的具体情况）

```
#include<bits/stdc++.h>
using namespace std;

const int N = 20;
int a[N][N], dp[N][N], ans[N];




int main()
{
	
	int n, m;
	cin >> n >> m;
	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= m; j++)
		{
			cin >> a[i][j];
		}
	}

	for (int i = 1; i <= n; i++)
	{
		for (int j = m; j >= 0; j--)
		{
			for (int k = 0; k <= m; k++)
			{
				if (j >= k)
				{
					dp[i][j] = max(dp[i][j], dp[i - 1][j - k] + a[i][k]);
				}
			}
		}
	}
	
	cout << dp[n][m] << endl;
	int j = m;
	for (int i = n; i; i--)
	{
		for (int k = 0; k <= m; k++)
		{
			if (dp[i][j] == dp[i - 1][j - k] + a[i][k])
			{
				ans[i] = k;
				j -= k;
				break;
			}
		}
	}

	

	for (int i = 1; i <= n; i++)
	{
		cout << i << " " << ans[i] << endl;
	}
}
```



# 动态规划（树形背包问题）

```
#include<bits/stdc++.h>
using namespace std;

const int N = 105;
int v[N], w[N], e[N], ne[N], h[N], idx;
int dp[N][N];
int n, sv;
void add(int a, int b)
{
	e[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

void dfs(int u)
{
	for (int i = h[u]; i != -1; i = ne[i])
	{
		int son = e[i];
		dfs(son);

		for (int j = sv - v[u]; j >= 0; j--)//枚举体积
		{
			for (int k = 0; k <= j; k++)//枚举分给该子树的体积
			{
				dp[u][j] = max(dp[u][j], dp[u][j - k] + dp[son][k]);
			}
		}//这一部分相当于对该结点的子树进行背包dp选一个最大值
	}

	for (int i = sv; i >= v[u]; i--)dp[u][i] = dp[u][i - v[u]] + w[u]);//在把当前的结点选上，这里相当于对根节点进行最后的背包dp选最大值

	for (int i = 0; i < v[u]; i++)dp[u][i] = 0;
	//小于父节点体积的部分，因为放不进去父结点，自然父节点的子树的方案也不存在所以是0
}
int main()
{
	memset(h, -1, sizeof(h));
	cin >> n >> sv;
	int fa, root;
	for (int i = 1; i <= n; i++)
	{
		cin >> v[i] >> w[i] >> fa;
		if (fa != -1)
		{
			add(fa, i);
		}
		else
		{
			root = i;
		}
	}

	dfs(root);
	cout << dp[root][sv] << endl;
}
```



# 动态规划背包问题求体积不超过v的状态下的方案数

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 1003;
const int mod = 1e9 + 7;
int dp[N], ans[N];


int main()
{
	int n, V;
	scanf("%d%d", &n, &V);
	ans[0] = 1;
	for (int i = 0; i < n; i++)
	{
		int v, w;
		scanf("%d%d", &v, &w);
		for (int j = V; j >= v; j--)
		{
			if (dp[j] < dp[j - v] + w)ans[j] = ans[j - v];
			if (dp[j] == dp[j -v] + w)ans[j] = (ans[j] + ans[j - v]) % mod;
			dp[j] = max(dp[j], dp[j - v] + w);
		}
	}
	int res = 0;
	for (int i = 0; i <= V; i++)res = max(res, dp[i]);
	int temp = 0;
	for (int i = 0; i <= V; i++)
	{
		if (dp[i] == res)temp = (temp + ans[i]) % mod;
	}
	printf("%d\n", temp);
}
```



# 线性DP（数字三角形）

```
//给定一个矩阵，每一行的元素个数是其对应行数，从下往上每次只能从相邻的斜线往上走，求权重最长的路径的值
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 503;
int a[N][N], dp[N][N];//自下而上到达第i,j位置时的路径的权重的最大值

int main()
{
	int n;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= i; j++)
		{
			scanf("%d", &a[i][j]);
		}
	}
	for (int i = 1; i <= n; i++)dp[n][i] = a[n][i];

	for (int i = n - 1; i; i--)
	{
		for (int j = 1; j <= i; j++)
		{
			dp[i][j] = max(dp[i + 1][j], dp[i + 1][j + 1]) + a[i][j];
		}
	}

	printf("%d\n", dp[1][1]);
}
```



# 线性DP（数字三角形模型）

```
//方格图，走两遍，走过的路权值变为0，问走完后的路径最短且权值最大，对于该模型，即使走过的路径不得二次经过也可以使用
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 12;
int dp[2*N][N][N];
//对于最开始我们可以建立一个四维数组同时对两个路径进行dp,因为两条路径同步则有x1+y1=x2+y2
//因此我们可以优化一维，保留x1,x2,新加一个k表示x1+y1的值
int w[N][N];

int main()
{
	int n;
	scanf("%d", &n);

	int x, y, a;
	while (scanf("%d%d%d", &x, &y, &a), x || y || a)w[x][y] = a;

	for (int k = 2; k <= 2 * n; k++)
	{
		for (int x1 = 1; x1 <= n; x1++)
		{
			for (int x2 = 1; x2 <= n; x2++)
			{
				int y1 = k - x1, y2 = k - x2;
				if (y1 >= 1 && y1 <= n && y2 >= 1 && y2 <= n)
				{
					int t = dp[k - 1][x1 - 1][x2];
					t = max(t, dp[k - 1][x1 - 1][x2 - 1]);
					t = max(t, dp[k - 1][x1][x2]);
					t = max(t, dp[k - 1][x1][x2 - 1]);
					t = t + w[x1][y1];
					if (x1 != x2)t = t + w[x2][y2];
					dp[k][x1][x2] = t;
				}
			}
		}
	}

	printf("%d\n", dp[2 * n][n][n]);

}
```



# 线性DP（最长上升子序列）

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 1005;
int a[N], dp[N];//数组，记录以j为结尾的最长非连续子序列的长度

int main()
{
	int n;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d", &a[i]);
	}
	
	for (int i = 1; i <= n; i++)
	{
		dp[i] = 1;
		for (int j = 1; j < i; j++)
		{
			if (a[j] < a[i])dp[i] = max(dp[i], dp[j] + 1);
		}
	}
	int res = 0;
	for (int i = 1; i <= n; i++) res = max(res, dp[i]);
	printf("%d\n", res);
}
```

# 线性DP（最长上升子序列模型）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 1003;
int a[N], dp1[N], dp2[N];

int main()
{
	int n;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)scanf("%d", &a[i]);

	for (int i = 1; i <= n; i++)
	{
		dp1[i] = 1;
		for (int j = 1; j < i; j++)
		{
			if (a[i] > a[j])dp1[i] = max(dp1[i], dp1[j] + 1);
		}
	}

	for (int i = n; i >= 1; i--)
	{
		dp2[i] = 1;
		for (int j = n; j > i; j--)
		{
			if (a[i] > a[j])dp2[i] = max(dp2[i], dp2[j] + 1);
		}
	}

	int ans = 0;

	for (int i = 1; i <= n; i++)
	{
		int res = dp1[i];
		for (int j = n; j > i; j--)
		{
			if (a[i] != a[j])res = max(res, dp1[i] + dp2[j]);
		}
		ans = max(res, ans);
	}

	printf("%d\n", n - ans);
}
```



# 线性DP（Dilworth定理）

```
//把序列分成不升子序列的最少个数，等于序列的最长上升子序列长度
//把序列分成不降子序列的最少个数，等于序列的最长下降子序列长度
//对于每个数，既可以把它接到已有子序列后面，也可以建立一个新序列。要使子序列数最少，应尽量不建立新序列。此外，应让每个子序列的末尾尽可能大，这样能接的数更多。因为一个数若能接到小数后面，必然能接到大数后面，反之则不成立。根据这些想法，可总结出如下贪心流程：
//从前往后扫描每个数，对于当前数
若现有子序列的结尾都小于它，则创建新子序列
否则，将它放到结尾大于等于它的最小数后面
//每一轮决策都使得现有的子序列可以尽可能的长
//无后效性是指如果在某个阶段上过程的状态已知，则从此阶段以后过程的发展变化仅与此阶段的状态有关，而与过程在此阶段以前的阶段所经历过的状态无关。利用动态规划方法求解多阶段决策过程问题，过程的状态必须具备无后效性。


#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 1003;
int a[N], dp1[N], dp2[N], idx;

int main()
{
	string s;
	getline(cin, s);
	stringstream ss(s);
	string s1;
	while (ss >> s1)
	{
		a[idx++] = stoi(s1);
	}
	int res = 0, ans = 0;
	for (int i = 0; i < idx; i++)
	{
		dp1[i] = 1, dp2[i] = 1;
		for (int j = 0; j < i; j++)
		{
			if (a[i] <= a[j])dp1[i] = max(dp1[i], dp1[j] + 1);
			else dp2[i] = max(dp2[i], dp2[j] + 1);
		}
		ans = max(ans, dp1[i]);
		res = max(res, dp2[i]);
	}
	printf("%d\n%d\n", ans, res);
}
```

# 线性DP（最少单调子序列数）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 53;
int a[N], up[N], down[N], n, ans;

void dfs(int u, int su, int sd)//枚举到第几个数，，最小上升子序列的个数，最小下降子序列的个数
{
	if (su + sd >= ans)return;
	if (u == n)
	{
		ans = min(ans, su + sd);
		return;
	}

	//放到上升子序列中,小于当前数的最大结尾的后面
	int k = upper_bound(up, up + su, a[u], greater<int>()) - up;
	if (k < su)
	{
		int t = up[k];
		up[k] = a[u];
		dfs(u + 1, su, sd);
		up[k] = t;
	}
	else
	{
		up[k] = a[u];
		dfs(u + 1, su + 1, sd);
	}

	//放到下降子序列中，大于当前数的最小结尾后面
	k = upper_bound(down, down + sd, a[u]) - down;
	if (k < sd)
	{
		int t = down[k];
		down[k] = a[u];
		dfs(u + 1, su, sd);
		down[k] = t;
	}
	else
	{
		down[k] = a[u];
		dfs(u + 1, su, sd + 1);
	}
}


int main()
{
	while (scanf("%d", &n), n)
	{
		for (int i = 0; i < n; i++)scanf("%d", &a[i]);
		ans = n;
		up[0] = INT_MAX;
		down[0] = INT_MIN;
		dfs(0, 0, 0);
		printf("%d\n", ans);
	}
}
```



# 线性DP（最长上升子序列二分优化）

```
对于任意长度下的子序列结尾值的最小值是严格单调递增，对于任意符合条件长度为l的子序列，倘若存在，则一定存在l-1长度的符合条件的子序列
l-1的子序列能够多接一个数，则必然存在l-1长度下的结尾值小于l长度下的结尾值，此条件一定成立，当且仅当l-1长度结尾值的最小值小于l长度下的结尾值的最小值
我们用一个数组q记录当前长度下结尾值的最小值，对于数组吧元素ai，如果q[len]<ai,则q[len+1]=a[i],否则寻找q[len]里面第一个大于等于ai的数，并用ai去更新

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 1e5 + 5;
int a[N], q[N];
int main()
{

	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &a[i]);
	}
	q[0] = -2e9;
	int len = 0;
	for (int i = 0; i < n; i++)
	{
		if (q[len] < a[i])q[++len] = a[i];
		else
		{
			int l = 0, r = len;
			while (l < r)
			{
				int mid = l + r >> 1;
				if (q[mid] >= a[i])r = mid;
				else l = mid + 1;
			}
			q[l] = a[i];
		}
	}
	printf("%d\n", len);
}

```

# 线性DP（最长公共子序列）

```
对于两个字符串A B，求两个字符串的最长公共子序列。
分析：状态表示，f(i,j)表示到A字符串第i个位置，到B字符串的第j个位置的最长公共子序列
集合划分，(!ai,!bj),(ai,!bj),(!ai,bj),(ai,bj),对于这四种情况求最大值即可，
其中要注意集合有重复部分但不影响求最大值
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1003;
int dp[N][N];

int main()
{
	int len1, len2;
	string a, b;
	cin >> len1 >> len2 >> a >> b;
	a = ' ' + a;
	b = ' ' + b;
	for (int i = 1; i < a.size(); i++)
	{
		for (int j = 1; j < b.size(); j++)
		{
			dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);//dp[i-1][j-1]的情况已经包含在这里面
			if (a[i] == b[j])dp[i][j] = max(dp[i][j], dp[i - 1][j - 1] + 1);//包含i和j的情况
		}
	}
	printf("%d\n", dp[len1][len2]);
}
```



# 线性DP（最长公共上升子序列暴力法）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 3003;
int n, a[N], b[N], dp[N][N];//a数组总从i个数选，b数组中以b[j]结尾的最长公共上升子序列\

//暴力做法
//分成两类，包含ai和不包含ai,其中包含ai的类里,对最长公共上升子序列里的倒数第二个进行枚举，找出最大的

int main()
{
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)scanf("%d", &a[i]);
	for (int i = 1; i <= n; i++)scanf("%d", &b[i]);

	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= n; j++)
		{
			dp[i][j] = dp[i - 1][j];
			if (a[i] == b[j])
			{
				int maxv = 1;
				for (int k = 1; k < j; k++)
				{
					if (b[k] < b[j])
					{
						maxv = max(maxv, dp[i - 1][k] + 1);
					}
				}
				dp[i][j] = max(dp[i][j], maxv);
			}
		}
	}
	
	int res = 0;
	for (int i = 1; i <= n; i++)res = max(dp[n][i], res);

	printf("%d\n", res);
}
```

# 线性DP（最长公共上升子序列优化版）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 3003;
int n, a[N], b[N], dp[N][N];//a数组总从i个数选，b数组中以b[j]结尾的最长公共上升子序列\

//预处理前j个数的最大值
//分成两类，包含ai和不包含ai,其中包含ai的类里,对最长公共上升子序列里的倒数第二个进行枚举，找出最大的

int main()
{
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)scanf("%d", &a[i]);
	for (int i = 1; i <= n; i++)scanf("%d", &b[i]);

	for (int i = 1; i <= n; i++)
	{
		int maxv = 1;
		for (int j = 1; j <= n; j++)
		{
			dp[i][j] = dp[i - 1][j];
			if (a[i] == b[j])dp[i][j] = max(maxv, dp[i][j]);

			if (b[j] < a[i])maxv = max(maxv, dp[i - 1][j] + 1);//对于所有满足条件的子序列导数第二个去最大值
		}
	}
	
	int res = 0;
	for (int i = 1; i <= n; i++)res = max(dp[n][i], res);

	printf("%d\n", res);
}
```



# 线性DP（最短编辑距离）

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1003;
int dp[N][N];//记录a字符串前i个字符跟b字符串前j个字符匹配上时的最小值

int main()
{
	int len1, len2;
	string a, b;
	cin >> len1 >> a >> len2 >> b;
	a = ' ' + a;
	b = ' ' + b;
	for (int i = 0; i < a.size(); i++)
	{
		dp[i][0] = i;//a的前i个字符和b的前0个字符匹配上所需的步数，即删掉前i个字符
	}
	for (int i = 0; i < b.size(); i++)
	{
		dp[0][i] = i;//a的前0个字符匹配上b的前i个字符，即给a添加i个字符
	}
	for (int i = 1; i < a.size(); i++)
	{
		for (int j = 1; j < b.size(); j++)
		{
			dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + 1;
			if (a[i] == b[j])dp[i][j] = min(dp[i][j], dp[i - 1][j - 1]);
			else dp[i][j] = min(dp[i][j], dp[i - 1][j - 1] + 1);
		}
	}
	printf("%d\n", dp[len1][len2]);
}
```



# 区间DP

```2
分析：集合是从i到j区间范围内合并的最小值
状态转移方程：min(dp[i][k]+dp[k+1][j])k=i,i+1,i+2,j

#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 303;
int s[N], dp[N][N];

int main()
{
	int n, x;
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d", &x);
		s[i] = s[i - 1] + x;
	}
	for (int len = 2; len <= n; len++)//区间长度为0时代价为0不用枚举
	{
		for (int i = 1; i + len - 1 <= n; i++)
		{
			int j = i + len - 1;
			dp[i][j] = 2e6 + 8;
			for (int k = i; k < j; k++)
			{
				dp[i][j] = min(dp[i][k] + dp[k + 1][j] + s[j] - s[i - 1], dp[i][j]);
			}
		}
	}
	printf("%d\n", dp[1][n]);
}

```



# 计数类DP

```
给定一个数，将这个数拆解成若干个数的和的形式，问拆解的方案数
转化为完全背包问题，改变集合属性为选法数量即可


#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N = 1003, mod = 1e9 + 7;
int dp[N];//数字n的选法数量

int main()
{
	int n;
	scanf("%d", &n);
	dp[0] = 1;
	for (int i = 1; i <= n; i++)
	{
		for (int j = i; j <= n; j++)
		{
			dp[j] = (dp[j] + dp[j - i]) % mod;
		}
	}

	printf("%d\n", dp[n]);
}
```



# 数位DP

```
//给定两个整数a,b求a到b的范围内的数字中含0~9的数字个数有多少个
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int get(vector<int>num, int l, int r)
{
	int ans = 0;
	for (int i = l; i >= r; i--)
	{
		ans = ans * 10 + num[i];
	}
	return ans;
}//用于计算数字字符串中指定区间范围内的数字值

int counts(int n, int t)//用于返回从
{
	vector<int>num;
	while (n)
	{
		num.push_back(n % 10);
		n /= 10;
	}
	int ans = 0;
	for (int i = num.size() - 1 - !t; i >= 0; i--)
	{
		if (i < num.size() - 1)
		{
			ans += get(num, num.size() - 1, i + 1) * pow(10, i);
			if (!t)ans -= pow(10, i);
		}
		if (num[i] == t)ans += get(num, i - 1, 0) + 1;
		else if (num[i] > t)ans += pow(10, i);
	}
	return ans;
}

int main()
{
	int a, b;
	while (cin >> a >> b, a)
	{
		if (a > b)swap(a, b);
		for (int i = 0; i <= 9; i++)
		{
			printf("%d ", counts(b, i) - counts(a - 1, i));
		}
		puts("");
	}
}
```



# 状压DP（棋盘式）

```
核心：先放横着的，再放竖着的
总方案数：只放横着的的合法方案数
判断，剩余位置能否充满竖着的小方块，可以按列来看，每一列内部所有连续的空着的小方块需要时偶数个
状态表示：dp[i][j]表示前i-1列已经摆好，且从第i-1列延伸至第i列的所有方案的状态是j的方案数,j用二进制数表示选还是未选，其中j是一个二进制数，表示当前这一行是否从i-1列延申至第i列

#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 12, M = 1 << N;
ll dp[N][M];
//dp[i][j]表示前i-1列已经摆好，且从第i-1列延伸至第i列的所有方案的状态是j的方案数,j用二进制数表示选还是未选，其中j是一个二进制数，表示当前这一行是否从i-1列延申至第i列
bool st[M];//判断状态合法性
vector<int>state[M];//跟状态M相匹配的装态集合
int n, m;
int main()
{
	while (cin >> n >> m, n || m)
	{
		memset(st, 1, sizeof(st));
		for (int i = 0; i < 1 << n; i++)
		{
			int cnt = 0;
			for (int j = 0; j < n; j++)
			{
				if (i >> j & 1)
				{
					if (cnt & 1)
					{
						st[i] = false;
						break;
					}
					cnt = 0;
				}
				else cnt++;
			}
			if (cnt & 1)st[i] = false;
		}//预处理st数组，用于记录该二进制状态是否存在有连续的奇数的零位存在，因为未被选的部分需要用竖的两个小方块去填

		for (int i = 0; i < 1 << n; i++)
		{
			state[i].clear();
			for (int j = 0; j < 1 << n; j++)
			{
				if (!(i & j) && st[i | j])//如果上一列的状态里对应的那个被占用的方块，因为那个方块衍生出来刚好占下当前这一列的那一块
				{
					state[i].push_back(j);
				}
			}
		}

		memset(dp, 0, sizeof(dp));
		dp[0][0] = 1;
		for (int i = 1; i <= m; i++)
		{
			for (int j = 0; j < 1 << n; j++)
			{
				for (auto k : state[j])
				{
					dp[i][j] += dp[i - 1][k];
				}
			}
		}

		printf("%lld\n", dp[m][0]);
	}
}


```



# 状压DP（最短哈密顿回路）

```
#include<bits/stdc++.h>
using namespace std;

const int N = 20, M = 1 << N;
int w[N][N];
int dp[M][N];//从0走到第j个点走过的点的状态是i的距离最小值
int n;

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			scanf("%d", &w[i][j]);
		}
	}

	memset(dp, 0x3f, sizeof(dp));
	dp[1][0] = 0;

	for (int i = 0; i < 1 << n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			if (i >> j & 1)
			{
				for (int k = 0; k < n; k++)
				{
					if (i - (1 << j) >> k & 1)
					{
						dp[i][j] = min(dp[i][j], dp[i - (1 << j)][k] + w[k][j]);
					}
				}
			}
		}
	}

	printf("%d\n", dp[(1 << n) - 1][n - 1]);
}
```



# 树形DP

```
#include<bits/stdc++.h>
using namespace std;

const int N = 6005;
int a[N], h[N], e[N], ne[N], idx;
int n;
bool st[N];
int dp[N][2];//以i位父节点的子树的方案，用0和1表示父节点i是否被选择，属性最大值

void add(int a, int b)
{
	e[idx] = b;
	ne[idx] = h[a];
	h[a] = idx++;
}

void dfs(int u)
{
	dp[u][1] = a[u];
	
	for (int i = h[u]; i != -1; i = ne[i])
	{
		int j = e[i];

		dfs(j);

		dp[u][0] += max(dp[j][0], dp[j][1]);
		dp[u][1] += dp[j][0];
	}
}

int main()
{
	scanf("%d", &n);
	for (int i = 1; i <= n; i++)
	{
		scanf("%d", &a[i]);
	}

	memset(h, -1, sizeof(h));

	for (int i = 1; i < n; i++)
	{
		int a, b;
		scanf("%d%d", &a, &b);
		add(b, a);
		st[a] = true;
	}

	int root = 1;
	while (st[root])root++;//如果当前结点存在父节点就++

	dfs(root);
	
	cout << max(dp[root][0], dp[root][1]);
	
}
```



# RMQ/ST表

```
//查询区间最值问题
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;

const int N = 2e5 + 3;
const int M = 18;

int dp[N][M];
//从i开始长度为2^j的区间的最大值
int a[N];
int n, q;

void init()
{
	for (int j = 0; j < M; j++)
	{
		for (int i = 1; i + (1 << j) - 1 <= n; i++)
		{
			if (!j)dp[i][j] = a[i];
			else dp[i][j] = max(dp[i][j - 1], dp[i + (1 << (j - 1))][j - 1]);
		}
	}
}

int query(int l, int r)
{
	int len = r - l + 1;
	int k = log(len) / log(2);

	return max(dp[l][k], dp[r - (1 << k) + 1][k]);
}

int main()
{
	ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

	cin >> n;
	for (int i = 1; i <= n; i++)cin >> a[i];

	cin >> q;
	init();
	while (q--)
	{
		int l, r;
		cin >> l >> r;
		cout << query(l, r) << "\n";
	}
}
```



# 记忆化搜索

```
#include<bits/stdc++.h>
using namespace std;

const int N = 303;
int a[N][N];
int dp[N][N];
int n, m;
int dir[4][2] = { 1,0,-1,0,0,1,0,-1 };

int memorized_search(int sx, int sy)
{
	if (dp[sx][sy] != -1)return dp[sx][sy];

	dp[sx][sy] = 1;
	for (int i = 0; i < 4; i++)
	{
		int x = sx + dir[i][0];
		int y = sy + dir[i][1];
		if (x > 0 && x <= n && y > 0 && y <= m && a[x][y] < a[sx][sy])
		{
			dp[sx][sy] = max(dp[sx][sy], memorized_search(x, y) + 1);
		}
	}
	
	return dp[sx][sy];
}

int main()
{
	scanf("%d%d", &n, &m);

	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= m; j++)
		{
			scanf("%d", &a[i][j]);
		}
	}

	memset(dp, -1, sizeof(dp));

	int res = 0;
	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= m; j++)
		{
			res = max(res, memorized_search(i, j));
		}
	}

	printf("%d\n", res);
	
}
```



# 记忆化搜索引例

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

ll a, b, c;
int dp[22][22][22];

ll w(ll a, ll b, ll c)
{
    if (a <= 0 || b <= 0 || c <= 0)return 1;
    if (a > 20 || b > 20 || c > 20)return w(20, 20, 20);
    if (dp[a][b][c])return dp[a][b][c];
    if (a < b && b < c)dp[a][b][c] = w(a, b, c - 1) + w(a, b - 1, c - 1) - w(a, b - 1, c);
    else dp[a][b][c] = w(a - 1, b, c) + w(a - 1, b - 1, c) + w(a - 1, b, c - 1) - w(a - 1, b - 1, c - 1);
    return dp[a][b][c];
}

int main()
{

    ios::sync_with_stdio(false), cin.tie(0), cout.tie(0);

    while (1)
    {
        cin >> a >> b >> c;
        if (a == -1 && b == -1 && c == -1)break;
        printf("w(%lld, %lld, %lld) = %lld\n", a, b, c, w(a, b, c));
    }
}
```



# 区间贪心（区间选点/最大不相交区间数量）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<int, int>PII;
const int N = 1e5 + 5;
int n;
PII p[N];

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		int l, r;
		scanf("%d%d", &l, &r);
		p[i].first = r;
		p[i].second = l;
	}

	sort(p, p + n);
	int ans = 1;
	int t = p[0].first;
	for (int i = 1; i < n; i++)
	{
		if (p[i].second > t)
		{
			ans++;
			t = p[i].first;
		}
	}
	printf("%d\n", ans);
}
```



# 区间贪心（区间分组，如果两个区间不相交，可以划为一组）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<int, int>PII;
const int N = 1e5 + 5;
int n;
PII p[N];

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		int l, r;
		scanf("%d%d", &l, &r);
		p[i].first = l;
		p[i].second = r;
	}

	sort(p, p + n);
	priority_queue<int, vector<int>, greater<int>>heap;//小根堆，用于存储每一组区间里的右端点的最大值

	for (int i = 0; i < n; i++)
	{
		if (!heap.size() || p[i].first <= heap.top())heap.push(p[i].second);
		else
		{
			heap.pop();
			heap.push(p[i].second);
		}
	}

	cout << heap.size() << endl;
}
```



# 区间贪心（区间覆盖）

```
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<int, int>PII;
const int N = 1e5 + 5;
int n;
PII p[N];

int main()
{
	int st, ed;
	scanf("%d%d", &st, &ed);
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		int l, r;
		scanf("%d%d", &l, &r);
		p[i].first = l;
		p[i].second = r;
	}

	sort(p, p + n);
	int res = 0;
	bool s = false;
	for (int i = 0; i < n; i++)
	{
		int j = i, r = -2e9;
		while (j < n && p[j].first <= st)
		{
			r = max(r, p[j].second);
			j++;
	
		}

		if (r < st)
		{
			res = -1;
			break;
		}

		res++;

		if (r >= ed)
		{
			s = true;
			break;
		}
		i = j - 1;
		st = r;
	}
	if (!s)res = -1;
	printf("%d\n", res);
	
}
```



# 哈夫曼树

```
//合并数字，每次合并的体力值是待合并的两个数的和，求合并完成后的最小值

#include<bits/stdc++.h>
using namespace std;


int main()
{
	int n;
	scanf("%d", &n);
	priority_queue<int, vector<int>, greater<int>>heap;
	while (n--)
	{
		int x;
		scanf("%d", &x);
		heap.push(x);
	}
	int res = 0;
	while (heap.size() > 1)
	{
		int a = heap.top(); heap.pop();
		int b = heap.top(); heap.pop();
		heap.push(a + b);
		res += a + b;
	}
	printf("%d\n", res);
}
```



# 经典贪心（等待时间问题）

```

//n个人打水，每个人有一个打水时间问所有人打完水的最短时间
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1e5 + 3;
int a[N];

int main()
{
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &a[i]);
	}
	sort(a, a + n);
	ll cnt = 0;
	ll ans = 0;
	for (int i = 0; i < n; i++)
	{
		ans += cnt;
		cnt += a[i];
	}
	printf("%lld\n", ans);
}
```



# 经典贪心（绝对值不等式，数轴距离问题）

```
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1e5 + 3;
int a[N];

int main()
{
	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		scanf("%d", &a[i]);
	}
	sort(a, a + n);
	int res = 0;
	for (int i = 0; i < n; i++)
	{
		res += abs(a[n / 2] - a[i]);
	}
	printf("%d\n", res);
}
```



# 经典贪心（推公式）

```
有n头牛，分别有两个数值，体重，强壮都，现在牛要叠罗汉，每头牛的危险系数等于他上面的牛的总重量减去他自身的强壮值，求整个叠罗汉的牛里危险系数最大值的最小值
问题分析：对于一个单独的决策分析，把一个决策里的第i头牛和第i+1头牛互换，看如何才能趋向最优解，得到公式当wi+si<wi+1+si+1时的方案才是最小值

#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<int, int>PII;
const int N = 5e4 + 3;
PII a[N];

int main()
{
	int n;
	scanf("%d", &n);
	for (int i = 0; i < n; i++)
	{
		int w, s;
		scanf("%d%d", &w, &s);
		a[i] = { w + s,w };
	}
	sort(a, a + n);
	
	int res = INT_MIN;
	int sum = 0;
	for (int i = 0; i < n; i++)
	{
		int w = a[i].second;
		int s = a[i].first - w;
		res = max(res, sum - s);
		sum += w;
	}

	printf("%d\n", res);

}
```



# Manacher

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int len[2515];/*该角标为中心所产生的回文字符串到右端点的距离*/
string init(string s)
{
	string str = "";
	str += "@";/*第一位补位防止越界*/
	for (int i = 0; i < s.size(); i++)
	{
		str += "#";
		str += s[i];
	}
	str += "#";
	str += "^";/*最后一位补位，防止越界*/
	/*字符串补位，前后补了一个无关字符是为了防止第37行代码越界*/
	return str;
}
void Manacher(string s)
{
	int valmx = 0;/*当前计算的回文串的右端点，一般来说是当下的最大值*/
	int idmx = 0;/*当前计算点（最大值）的中心角标*/
	int ans = 0;/*记录最大值答案*/
	for (int i = 1; i < s.size() - 1; i++)
	{
		if (i < valmx)
		{
			len[i] = min(valmx - i, len[2 * idmx - i]);
		}
		/*判断是否在最大回文串的内部，如果该点在回文串内部的对称点的数据已经更新，*/
		/*则拿对称点的数据和该点回文串长度的最小值比较，如果没更新则为零* /
		/*在该点的对称点数据已经刷新的情况下，对于一个在回文串内部的点*/
		/*他的一半长度一定小于等于右端点到该点长度的，但也有可能大于，大于的部分将会通过下面的程序更新数据*/
		else
		{
			len[i] = 1;
		}/*如果这个点在先有最大回文串的外边，则他的数据直接更新为1，并在下一行进行长度的最终赋值*/
		while (s[i-len[i]] == s[i+len[i]])
		{
			len[i]++;
		}/*判断该点回文串的最大长度*/
		if (len[i] + i > valmx)
		{
			valmx = len[i] + i;
			idmx = i;
		}/*如果该回文串并没有被当前回文串所包括，则重置待处理的回文串的右端点和中心点坐标*/
		ans = max(ans, len[i]);/*更新最大的回文串的长度*/
	}
	cout << ans-1 << endl;
}
int main()
{
	string s;
	getline(cin, s);
	Manacher(init(s));
	return 0;
}
```

