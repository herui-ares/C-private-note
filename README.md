# C-private-note
This is my personal notes about C Plus Plus. Please quit there, if you came in accidentally. 
**定义函数的参数传入**

注意取址符号

```c++
frontTree(TreeNode* cur, int i, string s, vector<int>& res){

};
```

**用迭代器建立哈希表**

```c++
unordered_set<int> ins_set(nums1.begin(), nums1.end());
```

**将集合做数组返回**

```c++
return vector<int>(res_set.begin(), res_set.end());
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

<img src="D:\softinstall\Typora\Typora\队列1.png" alt="队列1" style="zoom:50%;" />

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

<img src="D:\softinstall\Typora\Typora\队列2.png" alt="队列2" style="zoom:50%;" />

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

<img src="D:\softinstall\Typora\Typora\满二叉树.jpg" alt="满二叉树" style="zoom: 25%;" />

**完全二叉树**

设二叉树的深度为h，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最大个数，
第 h 层所有的结点都连续集中在最左边

<img src="D:\softinstall\Typora\Typora\完全二叉树.jpg" alt="完全二叉树" style="zoom: 25%;" />

满二叉树肯定是完全二叉树，而完全二叉树不一定是满二叉树。

- **二叉搜索树** 

它或者是一棵空树，或者是具有下列性质的[二叉树](https://baike.baidu.com/item/二叉树/1602879)： 若它的左子树不空，则左子树上所有结点的值均小于它的[根结点](https://baike.baidu.com/item/根结点/9795570)的值； 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值；

**平衡二叉树**

任意节点的子树的高度差都小于等于1。

**遍历方式**

<img src="D:\softinstall\Typora\Typora\二叉树.jpg" alt="二叉树" style="zoom: 33%;" />

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

<img src="D:\softinstall\Typora\Typora\二叉树1.png" alt="二叉树1" style="zoom:60%;" />

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
```

