# C-private-note
This is my personal notes about C Plus Plus. Please quit there, if you came in accidentally. The notes will be continually updated.

**C++万能头文件**

```c++
#include<bits/stdc++.h>
```

**函数变量英文命名**

**虚拟头结点 dummyHead**

如果题目要求链表需要前节点操作，则用虚拟链表

```c++
ListNode* dumyHead = new ListNode(0);
dumyHead->next = head;
```



**vector中没有find(), map和set中有**139题中先将vector<string> 复制在set中，用find查找

**string insert/erase**  leetcode93

```c++
string s = "abcde";
int i = 1;
s.insert(i + 1, ".");//插入字符串
//或者用迭代器
s.insert(s.begin() + i + 1, '.');//插入字符
s.erase(i + 1, 1); 
```

**C++运算符优先级列表**
![优先级](D:\softinstall\Typora\Typora\优先级.jpg)

**定义函数的参数传入**

注意取址符号

```c++
frontTree(TreeNode* cur, int i, string s, vector<int>& res){

};
```
### **STL**标准库函数

#### 顺序容器

顺序容器有以下三种：可变长动态数组 vector、双端队列 deque、双向链表 list。

#### 关联容器

关联容器有以下四种：set、multiset、map、multimap。

所有容器都有以下两个成员函数：

- int size()：返回容器对象中元素的个数。
- bool empty()：判断容器对象是否为空。


 顺序容器和关联容器还有以下成员函数：

- begin()：返回指向容器中第一个元素的迭代器。
- end()：返回指向容器中最后一个元素后面的位置的迭代器。
- rbegin()：返回指向容器中最后一个元素的反向迭代器。
- rend()：返回指向容器中第一个元素前面的位置的反向迭代器。
- erase(...)：从容器中删除一个或几个元素。该函数参数较复杂，此处省略。
- clear()：从容器中删除所有元素。


 如果一个容器是空的，则 begin() 和 end() 的返回值相等，rbegin() 和 rend() 的返回值也相等。

 顺序容器还有以下常用成员函数：

- front()：返回容器中第一个元素的引用。
- back()：返回容器中最后一个元素的引用。
- push_back()：在容器末尾增加新元素。
- pop_back()：删除容器末尾的元素。
- insert(...)：插入一个或多个元素。该函数参数较复杂，此处省略。

**哈希表也可以for用遍历**

```c++
unordered_map<char, int> ori, cnt;
for (auto& p : ori) {
     if (cnt[p.first] < ori[p.first]) {
        return false;
    }
}
```

**优先级队列**

```c++
priority_queue<int, vector<int>> pq;//默认的是vector<int>  并且是最大值优先队列，也可以用deque<int>
//也可以省略
priority_queue<int> pq;
priority_queue<int, vector<int>， greater<int>> pq; //最小值优先队列
// 定义一个小顶堆，大小为k
class mycomparison {
    public:
        bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
            return lhs.second > rhs.second;
        }
    };
priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pri_que;

```



**用迭代器建立哈希表**

```c++
unordered_set<int> ins_set(nums1.begin(), nums1.end());
```

**将集合做数组返回**

```c++
return vector<int>(res_set.begin(), res_set.end());
```
**拷贝vector**

```c++
//inorder = [3,9,20,15,7] inIndex = 1;
vector<int> inLeft(inorder.begin(), inorder.begin() + inIndex);
vector<int> inRight(inorder.begin() + inIndex + 1, inorder.end());
//则inLeft = [3]  注意并没有拷贝9
//inRight = [20,15,7]
```


**返回map中与temp相同元素的数量**

```c++
unordered_map<int, int> map;
res = map.count(temp);
```

**返回map中是否有temp的一个迭代器。Res->first为键，res->second为值，没有找到，返回map.end();**

```c++
res = map.find(temp);
```
**取hash表的值**

```c++
for(auto it = hashStr.begin(); it != hashStr.end(); it++) {
   res.push_back(it->second);
}
```


**移除s.begin()到i的字符串，其复杂度为O(n)**

```c++
s.erase(s.begin() + i);
```

**重新设置字符串大小**

```c++
s.resize(slowIndex);
```

**翻转字符串/数组** 

```c++
reverse(result.begin(), result.end());
```

**往数组最后添加元素** 

```c++
res.push_back(num);
```

**排序数组**

```c++
sort(result.begin(), result.end());
```

反向排序（大到小）

```c++
sort(result.begin(), result.end(), greater<int>());
```
**sort自定义规则**

```c++
//是vector的内置，string 不能用
必须得加static
static bool cmp(const int& a, const int& b) {
	return a > b; //从大到小排序  	//如果返回为真，则将第一个数放在前面
	//return a < b; //从 小到大排序
}
sort(nums.begin(), nums.end(), cmp);
sort(strs.begin(), strs.end(), [](string& x, string& y){ return x + y < y + x; });
sort(nums.begin(), nums.end(), [] (int& a, int& b)  {
            string stra = to_string(a);
            string strb = to_string(b);
            return  stra + strb < strb + stra;
        });
```


**单引号、双引号** 

- 单引号是字符型 char

- 双引号是字符串型 string

**字符串转数字** 

stoi,遇见非数字字符跳出

```c++
string a = "1234a"
int res = stoi(a);//res为1234
```

**字符转数字**  ？



**数字转字符**

```c++
char a = to_string(2);
```

**迭代器**

```c++
vector<int> inorder{9,3,15,20,7};
int index = 1;
vector<int> leftIn(inorder.begin(), inorder.begin() + index);
// leftIn 中为 9;不包含3
vector<int> rightIn(inorder.begin() + index + 1, inorder.end());
// rightIn 中为 15,20,7;
```



# 二分法

**版本一**

定义 target 是在一个在左闭右闭的区间里，也就是[left, right] （这个很重要非常重要）。区间的定义这就决定了二分法的代码应该如何写，因为定义target在[left, right]区间，所以有如下三点：

- right = nums.size() - 1;

- while (left <= right) 要使用 <= ，因为left == right是有意义的，所以使用 <=
- if (nums[middle] > target) right 要赋值为 middle - 1，因为当前这个nums[middle]一定不是target，那么接下来要查找的左区间结束下标位置就是 middle - 1。

**版本二**

定义 target 是在一个在左闭右开的区间里，也就是[left, right) ，有如下三点：

- right = nums.size()；

- while (left < right)，这里使用 < ,因为left == right在区间[left, right)是没有意义的

- if (nums[middle] > target) right 更新为 middle，因为当前nums[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums[middle]。

# KMP

解决一个字符串中是否出现过另一个字符串问题，或者类似重复子字符串问题

**前缀表next数组**  

```c++
    vector<int> getNext(string s){
        int slen = s.length();
        vector<int> next(slen); 
        int j = -1;
        next[0] = j;
        for(int i = 1; i < slen; i++){
            while(j >= 0 && s[i] != s[j + 1]){
                j = next[j];
            }
            if(s[i] == s[j + 1]){
                j++;
            }
            next[i] = j;
        }
        return next;
    }
```

**栈** 

```c++
stack<int> stIn
```

- push(x) -- 元素 x 入栈
- pop() -- 移除栈顶元素
- top() -- 获取栈顶元素
- empty() -- 返回栈是否为空
- size() -- 返回栈中元素的个数

**队列** 

```c++
queue<int> que1;
```

![image](https://github.com/herui-ares/C-private-note/blob/main/%E9%98%9F%E5%88%971.png)

- push(x) -- 将一个元素放入队列的尾部。
- pop() -- 从队列首部移除元素。
- empty() -- 返回队列是否为空。
- size() -- 返回队列中元素的个数。
- front() -- 返回队首元素的元素，但不删除该元素。
- back() -- 返回队列尾元素的元素，但不删除该元素。

**双端队列** 

```c++
deque<int> que;
```

![image](https://github.com/herui-ares/C-private-note/blob/main/%E9%98%9F%E5%88%972.png)

- push_back(elem);//在容器尾部添加一个数据
- push_front(elem);//在容器头部插入一个数据
- pop_back();//删除容器最后一个数据
- pop_front();//删除容器第一个数据
- front()：返回 queue 中第一个元素的引用。
- back()：返回 queue 中最后一个元素的引用。
- size()：返回 queue 中元素的个数。
- empty()：如果 queue 中没有元素的话，返回 true。

**this** 

在 C++ 中，每一个对象都能通过 **this** 指针来访问自己的地址。**this** 指针是所有成员函数的隐含参数。因此，在成员函数内部，它可以用来指向调用对象。

```c++
class MyQueue {
public:
    stack<int> stIn;
    stack<int> stOut;
    /** Initialize your data structure here. */
    MyQueue() {
    }    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        ////////////
    }
    /** Get the front element. */
    int peek() {
        int res = this->pop();// this直接使用已有的pop函数
        stOut.push(res);
        return res;
    }
};
```

**递归三要素**

1. **「确定递归函数的参数和返回值：」**确定哪些参数是递归的过程中需要处理的，那么就在递归函数里加上这个参数， 并且还要明确每次递归的返回值是什么进而确定递归函数的返回类型。
2. **「确定终止条件：」**写完了递归算法,  运行的时候，经常会遇到栈溢出的错误，就是没写终止条件或者终止条件写的不对，操作系统也是用一个栈的结构来保存每一层递归的信息，如果递归没有终止，操作系统的内存栈必然就会溢出。
3. **「确定单层递归的逻辑：」**确定每一层递归需要处理的信息。在这里也就会重复调用自己来实现递归的过程。

# **二叉树** 

**叶子节点**

指没有左右节点的节点

- **满二叉树**  

除最后一层无任何子[节点](https://baike.baidu.com/item/节点/865052)外，每一层上的所有结点都有两个子结点的二叉树。

国内教程定义：一个二叉树，如果每一个层的结点数都达到最大值，则这个二叉树就是满二叉树。也就是说，如果一个二叉树的层数为K，且结点总数是(2^k) -1 ，则它就是满二叉树。

![image](https://github.com/herui-ares/C-private-note/blob/main/%E6%BB%A1%E4%BA%8C%E5%8F%89%E6%A0%91.jpg)

**完全二叉树**

设二叉树的深度为h，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最大个数，
第 h 层所有的结点都连续集中在最左边


![image](https://github.com/herui-ares/C-private-note/blob/main/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91.jpg)

满二叉树肯定是完全二叉树，而完全二叉树不一定是满二叉树。

- **二叉搜索树** 

它或者是一棵空树，或者是具有下列性质的[二叉树](https://baike.baidu.com/item/二叉树/1602879)： 若它的左子树不空，则左子树上所有结点的值均小于它的[根结点](https://baike.baidu.com/item/根结点/9795570)的值； 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；

**平衡二叉树**

任意节点的子树的高度差都小于等于1。

**遍历方式**
![image](https://github.com/herui-ares/C-private-note/blob/main/%E4%BA%8C%E5%8F%89%E6%A0%91.jpg)

- 深度优先遍历：先往深走，遇到叶子节点再往回走。
  - 前序遍历（递归法，迭代法）1245367
  - 中序遍历（递归法，迭代法）4251637
  - 后序遍历（递归法，迭代法）4526731

- 广度优先遍历：一层一层的去遍历。
  - 层次遍历（迭代法）

**「如果需要搜索整颗二叉树，那么递归函数就不要返回值，如果要搜索其中一条符合条件的路径，递归函数就需要返回值，因为遇到符合条件的路径了就要及时返回。」**

**二叉树C++定义**

```c++
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
```

**创建一个二叉树root**

```c++
struct TreeNode {
	int val;
	TreeNode* left;
	TreeNode* right;
	TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
class BinTree
{
public:
    TreeNode* root;
	void CreateTree();
};

void BinTree::CreateTree()//创建一棵二叉树
{
	TreeNode* p1 = new TreeNode(6);
	TreeNode* p2 = new TreeNode(4);
	TreeNode* p3 = new TreeNode(7);
	TreeNode* p4 = new TreeNode(1);
	TreeNode* p5 = new TreeNode(3);
	TreeNode* p6 = new TreeNode(5);
	TreeNode* p7 = new TreeNode(8);
	p1->left = p2;
	p1->right = p3;
	p2->left = p4;
	p2->right = p5;
	p3->left = p6;
	p3->right = p7;
	root = p1;
}
```

**前序遍历递归**

```c++
class Solution {
public:
    void traversal(TreeNode* cur, vector<int>& vec) {
        if (cur == NULL) return;
        vec.push_back(cur->val);    // 中
        traversal(cur->left, vec);  // 左
        traversal(cur->right, vec); // 右
    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        traversal(root, result);
        return result;
    }
};
```

**中序遍历递归**

```c++
    void traversal(TreeNode* cur, vector<int>& vec) {
        if (cur == NULL) return;
        traversal(cur->left, vec);  // 左
        vec.push_back(cur->val);    // 中
        traversal(cur->right, vec); // 右
    }
```

**后续遍历递归**

```c++
  void traversal(TreeNode* cur, vector<int>& vec) {
    if (cur == NULL) return;
    traversal(cur->left, vec); // 左
    traversal(cur->right, vec); // 右
    vec.push_back(cur->val);  // 中
  }
```

**前序遍历迭代法**

```c++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> result;
        st.push(root);
        while (!st.empty()) {
            TreeNode* node = st.top();                      // 中
            st.pop();
            if (node != NULL) result.push_back(node->val);
            else continue;
            st.push(node->right);                           // 右
            st.push(node->left);                            // 左
        }
        return result;
    }
};
```

**中序遍历迭代法**

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        stack<TreeNode*> st;
        TreeNode* cur = root;
        while (cur != NULL || !st.empty()) {
            if (cur != NULL) { // 指针来访问节点，访问到最底层
                st.push(cur); // 讲访问的节点放进栈
                cur = cur->left;                // 左
            } else {
                cur = st.top(); // 从栈里弹出的数据，就是要处理的数据（放进result数组里的数据）
                st.pop();
                result.push_back(cur->val);     // 中
                cur = cur->right;               // 右
            }
        }
        return result;
    }
};
```

**后序遍历迭代法**

```c++
class Solution {
public:
  vector<int> postorderTraversal(TreeNode* root) {
    stack<TreeNode*> st;
    vector<int> result;
    st.push(root);
    while (!st.empty()) {
      TreeNode* node = st.top();
      st.pop();
      if (node != NULL) result.push_back(node->val);
      else continue;
      st.push(node->left); // 相对于前序遍历，这更改一下入栈顺序
      st.push(node->right);
    }
    reverse(result.begin(), result.end()); // 将结果反转之后就是左右中的顺序了
    return result;
  }
};
```

**层序遍历**

```c++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        if (root != NULL) que.push(root);
        vector<vector<int>> result;
        while (!que.empty()) {
            int size = que.size();
            vector<int> vec;
            // 这里一定要使用固定大小size，不要使用que.size()，因为que.size是不断变化的
            for (int i = 0; i < size; i++) {
                TreeNode* node = que.front();
                que.pop();
                vec.push_back(node->val);
                if (node->left) que.push(node->left);
                if (node->right) que.push(node->right);
            }
            result.push_back(vec);
        }
        return result;
    }
};
```

**二叉树最大深度、最小深度、节点**

![image](https://github.com/herui-ares/C-private-note/blob/main/%E4%BA%8C%E5%8F%89%E6%A0%911.png)

后序遍历

```c++
//最大深度(最大高度)最大高度与最大深度在数值上是一样的
class Solution {
public:
    int getDepth(TreeNode* node) {
        if (node == NULL) return 0;
        int leftDepth = getDepth(node->left);       // 左
        int rightDepth = getDepth(node->right);     // 右
        int depth = 1 + max(leftDepth, rightDepth); // 中
        return depth;
    }
    int maxDepth(TreeNode* root) {
        return getDepth(root);
    }
};
////////////////////////////////
//最小深度
class Solution {
public:
    int getDepth(TreeNode* node) {
        if (node == NULL) return 0;
        int leftDepth = getDepth(node->left);    // 左
        int rightDepth = getDepth(node->right);  // 右
                                                 // 中
        // 当一个左子树为空，右不为空，这时并不是最低点
        if (node->left == NULL && node->right != NULL) { 
            return 1 + rightDepth;
        }   
        // 当一个右子树为空，左不为空，这时并不是最低点
        if (node->left != NULL && node->right == NULL) { 
            return 1 + leftDepth;
        }
        int result = 1 + min(leftDepth, rightDepth); 
        return result;
    }
    int minDepth(TreeNode* root) {
        return getDepth(root);
    }
};
///////////////////////////////
//节点个数
class Solution {
private:
    int getNodesNum(TreeNode* cur) {
        if (cur == 0) return 0;
        int leftNum = getNodesNum(cur->left);      // 左
        int rightNum = getNodesNum(cur->right);    // 右
        int treeNum = leftNum + rightNum + 1;      // 中
        return treeNum;
    }
public:
    int countNodes(TreeNode* root) {
        return getNodesNum(root);
    }
};
///左叶子之和404， 指没有子节点的左节点。不是左侧节点的意思
class Solution {
public:
	int sumOfLeftLeaves(TreeNode* root) {
		if (root == nullptr) return 0;
		return clcleftSum(root);

	}
	int clcleftSum(TreeNode* cur) {
		if (cur == nullptr) return 0;
		int leftSum = clcleftSum(cur->left);
		int rightSum = clcleftSum(cur->right);
		int midValue = 0;
		if (cur->left && !cur->left->left && !cur->left->right) {
			midValue = cur->left->val;
		}
		int sum = leftSum + rightSum + midValue;
		return sum;
	}
};
```

真正的二叉树最大深度该采用前序遍历

```c++
class Solution {
public:
    int result;
    void getDepth(TreeNode* node, int depth) {
        result = depth > result ? depth : result; // 中
        if (node->left == NULL && node->right == NULL) return ;
        if (node->left) { // 左
            depth++;    // 深度+1
            getDepth(node->left, depth);
            depth--;    // 回溯，深度-1
        }
        if (node->right) { // 右
            depth++;    // 深度+1
            getDepth(node->right, depth);
            depth--;    // 回溯，深度-1
        }
        return ;
    }
    int maxDepth(TreeNode* root) {
        result = 0;
        if (root == 0) return result;
        getDepth(root, 1);
        return result;
    }
};
	//判断平衡二叉树（用最大高度）
class Solution {
public:
    // 返回以该节点为根节点的二叉树的高度，如果不是二叉搜索树了则返回-1
    int getDepth(TreeNode* node) {
        if (node == NULL) {
            return 0;
        }
        int leftDepth = getDepth(node->left);
        if (leftDepth == -1) return -1; // 说明左子树已经不是二叉平衡树
        int rightDepth = getDepth(node->right);
        if (rightDepth == -1) return -1; // 说明右子树已经不是二叉平衡树
        return abs(leftDepth - rightDepth) > 1 ? -1 : 1 + max(leftDepth, rightDepth);
    }
    bool isBalanced(TreeNode* root) {
        return getDepth(root) == -1 ? false : true; 
    }
};

```
