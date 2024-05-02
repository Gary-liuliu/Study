一 ：哈夫曼树的建立和遍历

```c++
#include<iostream>
#include<stdio.h>
using namespace std;
typedef struct
{
	int weight;
	int parent, lchild, rchild;
}HTNode, * HuffmanTree;

void Select(HuffmanTree HT, int len, int& s1, int& s2)
{
	int i, min1 = 0x3f3f3f3f, min2 = 0x3f3f3f3f;
	for (i = 1; i <= len; i++)
	{
		if (HT[i].weight < min1 && HT[i].parent == 0)
		{
			min1 = HT[i].weight;
			s1 = i;
		}
	}
	int temp = HT[s1].weight;
	HT[s1].weight = 0x3f3f3f3f;
	for (i = 1; i <= len; i++)
	{
		if (HT[i].weight < min2 && HT[i].parent == 0)
		{
			min2 = HT[i].weight;
			s2 = i;
		}
	}
	HT[s1].weight = temp;
}

void CreatHuffmanTree(HuffmanTree& HT, int n)
{
	//构造赫夫曼树HT
	int m, s1, s2, i;
	if (n <= 1) return;
	m = 2 * n - 1;
	HT = new HTNode[m + 1];  		  
	for (i = 1; i <= m; ++i)        	  
	{
		HT[i].parent = 0;  HT[i].lchild = 0;  HT[i].rchild = 0;
	}
	printf("请输入叶子结点的权值：\n");
	for (i = 1; i <= n; ++i)        	 
		cin >> HT[i].weight;
	for (i = n + 1; i <= m; ++i)
	{  
		Select(HT, i - 1, s1, s2);
		HT[s1].parent = i;
		HT[s2].parent = i;
		HT[i].lchild = s1;
		HT[i].rchild = s2;							
		HT[i].weight = HT[s1].weight + HT[s2].weight; 	
	}												
}

void Print(HuffmanTree HT,int n) {
	int m = 2 * n - 1;
	for (int i = 1; i <= m; i++) {
		printf("%d              %d            %d           %d       %d\n", i, HT[i].weight, HT[i].parent, HT[i].lchild, HT[i].rchild);
	}
}

void main()
{
	HuffmanTree HT;
	int n;
	cout << "请输入叶子结点的个数：\n";
	cin >> n;
	CreatHuffmanTree(HT, n);
	cout << "哈夫曼树建立完毕！\n";
	cout << "输出中。。。。\n";
	printf("结点         weight         parent       l      r\n");
	Print(HT, n);
}
```

二：FoodFill算法四连通问题

```c++
#include<cstring>
#include<iostream>
#include<algorithm>

using namespace std;

#define x first
#define y second
typedef pair<int, int > PII;
const int N = 300, M = N * N;
PII q[M];
bool st[N][N] = { false };

char g[N][N];

void bfs(int sx, int sy, int n, int m)
{
	int hh = 0; int tt = 0; int j, k;
	q[0] = { sx,sy };
	st[sx][sy] = true;
	int lx[4] = { -1,0,1,0 };
	int ly[4] = { 0,-1,0,1 };

	while (hh <= tt)
	{
		PII  t = q[hh++];
		for (int i = 0; i < 4; i++)
		{
			j = t.x + lx[i];
			k = t.y + ly[i];
			if (j < 0 || j >= n || k < 0 || k >= m)continue;
			if (g[j][k] == '0' || st[j][k])continue;
			q[++tt] = { j,k };
			st[j][k] = true;
		}
	}

}
int main() {
	int n, m;
	scanf("%d%d", &n, &m);
	for (int i = 0; i < n; i++) scanf("%s", g[i]); 
	int cnt = 0;
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < m; j++)
		{
			if (g[i][j] == '1' && st[i][j] == false)
			{
				bfs(i, j, n, m);
				cnt++;
			}
		}
	}
	printf("%d", cnt);
}
```

三：快速排序

~~~c++
#include <iostream>

using namespace std;

const int N = 1e5 + 10;

int q[N];           //注意要定义在main函数外面

void quick_sort(int q[], int l ,int r)
{
	if ( l >= r) return;

```c++
int i = l - 1, j = r + 1, x = q[l + r >> 1];
while (i < j) {
	do ++i ; while (q[i] < x);
	do --j ; while (q[j] > x);
	if (i < j) swap(q[i], q[j]);
}

quick_sort(q, l, j);
quick_sort(q, j + 1, r);
```

}

int main()
{
	int n;
	scanf("%d", &n);

	for (int i = 0; i < n; ++i) scanf("%d", &q[i]);
	
	quick_sort(q, 0, n - 1);
	
	for (int i = 0; i < n; ++i) printf("%d ", q[i]);
	return 0;

}
~~~

四：二叉树的建立

```c
#include<stdio.h>
#include <crtdbg.h>
#include <corecrt_malloc.h>

typedef struct BiNode{				//二叉链表定义
	char data;
	struct BiNode *lchild,*rchild;
}BiTNode,*BiTree;

void CreateBiTree(BiTree &T) {
	//按先序次序输入二叉树中结点的值（一个字符），创建二叉链表表示的二叉树T
	char ch;
	scanf_s("%c", &ch);
	if (ch == '#')  T = NULL;			//递归结束，建空树
	else {
		T = (BiTree)malloc(sizeof(BiTNode));
		T->data = ch;					//生成根结点
		CreateBiTree(T->lchild);	//递归创建左子树
		CreateBiTree(T->rchild);	//递归创建右子树
	}
}

void Traverseone(BiTree T)
{
	if (T != NULL)
	{
		printf("%c", T->data);
		Traverseone(T->lchild);
		Traverseone(T->rchild);
	}
}

void Traversetwo(BiTree T) {
	if (T != NULL) {
		Traversetwo(T->lchild);
		printf("%c", T->data);
		Traversetwo(T->rchild);
	}
}

void Traversetree(BiTree T)
{
	if (T != NULL)
	{
		Traversetree(T->lchild);
		Traversetree(T->rchild);
		printf("%c", T->data);
	}
}

int main()
{
	BiTree bitree;
	bitree = NULL;
	void CreateBiTree(BiTree & T); void Traverseone(BiTree T); void Traversetwo(BiTree T); void Traversetree(BiTree T);
	printf("输入数据:");
	CreateBiTree(bitree);
	printf("前序遍历:");
	Traverseone(bitree);
	printf("\n");
	printf("中序遍历:");
	Traversetwo(bitree);
	printf("\n");
	printf("后序遍历:");
	Traversetree(bitree);
}
```

五：图的建立和遍历

```c++
#include<iostream>
  
using namespace std;

#define MVNum 100 

typedef struct ArcNode {                	
	int adjvex;                          	
	struct ArcNode* nextarc;          		                      	
}ArcNode;

typedef struct VNode {
	char data;                    	
	ArcNode* firstarc;                		
}VNode, AdjList[MVNum];               		

typedef struct {
	AdjList vertices;                 		
	int vexnum, arcnum;              		
}ALGraph;

int LocateVid(ALGraph G, char v)
{
	for (int i = 0; i < G.vexnum; i++)
	{
		if (G.vertices[i].data == v)return i;
	}
	return -1;
}

void CreateIOE(ALGraph &G)
{
	cout << "输入顶点数  ";
	cin >> G.vexnum;
	cout << "输入边的数量  ";
	cin >> G.arcnum;
	cout << endl;
	cout << "----输入各个顶点---"<<endl;
	for (int i = 0; i < G.vexnum; i++)
	{
		cout << "输入第" << (i + 1) << "个顶点 ";
		cin >> G.vertices[i].data;
		G.vertices[i].firstarc = NULL;
	}
	cout << "----输入一条边香菱的两个顶点---"<<endl;
	for (int i = 0; i < G.arcnum; i++)
	{
		char v1, v2;
		cout << "输入第" << (i + 1) << "条边依附的顶点 ";
		cin >> v1 >> v2;
		int k = LocateVid(G, v1); int l = LocateVid(G, v2);
		ArcNode* p1 = new ArcNode;       
		//p1 = (ArcNode*)malloc(sizeof(ArcNode));
		//前插法
		p1->adjvex = k; 
		p1->nextarc = G.vertices[l].firstarc;  G.vertices[l].firstarc = p1;

		ArcNode* p2 = new ArcNode;
		p2->adjvex = l;
		p2->nextarc = G.vertices[k].firstarc; G.vertices[k].firstarc = p2;
	}

}

int main()
{
	ALGraph G;
	CreateIOE(G);

	cout << "输出。。。。" << endl;
for (int i = 0; i < G.vexnum; i++){VNode temp = G.vertices[i];ArcNode* p = temp.firstarc;if (p == NULL) {cout << G.vertices[i].data;cout << endl;}else {cout << temp.data;while (p) {cout << "->";cout << p->adjvex;p = p->nextarc;}}cout << endl;}

`}
```

六：全排列模板

```c++
#include<iostream>

using namespace std;

void swap(int& a, int& b)
{
	int r = a;
	a = b;
	b = r;
}

void prem(int* v, int k, int m)
{
	if (k == m)
	{
		for (int i = 0; i < m; i++)
		{
			cout << v[i] << " " ;
		}
		cout << endl;
	}
	else
	{
		for (int i = k; i < m; i++)
		{
			swap(v[i], v[k]);
			prem(v, k + 1, m);
			swap(v[i], v[k]);
		}
	}
}

int main()
{
	int n; int nums[1000];
	cin >> n;
	for (int i = 0; i < n; i++)
	{
		cin >> nums[i];
	}
	prem(nums, 0, n );
	return 0;
}
```

七：蓝桥杯日期

```C++
#include <bits/stdc++.h>

using namespace std;

int days[] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

bool is_leap(int y)
{
    return y % 400 == 0 || y % 4 == 0 && y % 100 != 0;
}

int dayofmanth(int y, int m)
{
    if (m == 2)
        return is_leap(y) + 28;
    return days[m];
}

void check(int y, int m, int d)
{
    
}
```

八：二维vector数组输入

```c++
    vector<vector<int>> g;
    vector<int> v;
    int n, nm, t;
    cin >> n >> nm;//一定要用>>隔开输入，不然就不是连续输入，而是作了运算
    for (int i = 0; i < n; i++)
    {
        v.clear();
        for (int j = 0; j < nm; j++)
        {
            cin >> t;
            v.push_back(t);
        }
        g.push_back(v);
    }
```

