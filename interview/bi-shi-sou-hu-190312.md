# 搜狐

> 问题不难,个人基础知识掌握得太不牢固了

## 问答题

1. 深度学习BN的作用

2. BN在神经网络中的位置

    全连接层以及卷积层之后,激活函数之前

3. ReLU的优点

4. Recall,Precision,ROC的概念
    
    ROC曲线可以表现学习器泛化性能的好坏.
    我们根据学习期的预测结果对样例进行排序,按此顺序逐个把样本作为正例进行预测,每次计算出两个重要量的值,分别以它们为横\纵坐标作图,就得到了ROC曲线.
    与P-R曲线使用查准率(Precision)\查全率(Recall)为纵\横轴不同,ROC曲线的纵轴是"真正例率"(TPR),横轴是"假正例率"(FPR),其计算方式为

    $$TPR=\frac{TP}{TP+FN}$$

    $$FPR=\frac{FP}{TN+FP}$$

5. 机器学习\深度学习常识


## 编程题

1. C++定位数组元素索引

> 在一个有重复元素的有序数组（从小到大）中，找到指定元素的索引（索引从0开始）。给定一个有重复元素的有序数组： int nums[], 一个int数值 target， 找不到则返回-1

2. C++二叉树路径搜索

> 给定一个二叉树和一个int型数值target，判断是不是有一条从根到叶子的路径，加和等于target

## 题解

1. 直接二分查找
```
#include<iostream>

using namespace std;

int find_index(const int nums[], int begin, int end, int target)
{
	
	if (target < nums[0] || target > nums[end])
		return -1;
	
	while (begin <= end)
	{
		int mid = (begin + end) / 2;

		if (target == nums[mid])
		{
			while (nums[mid] == target)
				mid--;
			return (mid+1);
		}
		else if (target > nums[mid])
			begin = mid + 1;
		else
			end = mid - 1;
	}
	return -1;
}

int main()
{
	int nums[] = { 0,1,1,1,2,3,3,3,4,4,4,6 };
	int target;
	int len = sizeof(nums) / sizeof(int);
	cin >> target;
	int i = find_index(nums, 0, len-1, target);
	cout << i << endl;
	return 0;
}
```

2. 递归

> 剑指Offer》第34题：二叉树中和为某一值的路径。

当用前序遍历的方式访问到某一节点时，把该节点添加到路径上，并累加该节点的值。如果该节点为叶节点，并且路径中节点值的和刚好等于输入的整数，则当前路径符合要求，将其保存到结果vector中。如果当前节点不是叶节点，则继续访问它的子节点。当前节点访问结束后，递归函数将自动回到它的父节点。因此，在函数退出之前要在路径上删除当前节点并减去当前节点的值，以确保返回父节点时路径刚好是从根节点到父节点。
不难看出，保存路径的数据结构实际上是一个栈，因为路径要与递归调用状态一致，而递归调用的本质就是一个压栈和出栈的过程。


```
#include<iostream>
#include<vector>

using namespace std;

class BinaryTree
{
public:
	int val;
	BinaryTree *pL_tree;
	BinaryTree *pR_tree;

	BinaryTree(int x) :val(x), pL_tree(nullptr), pR_tree(nullptr){};
};

void FindPath(BinaryTree* pRoot, 
			  int expectedSum, 
			  std::vector<int>& path, 
			  int& currentSum,
			  vector<vector<int>> &ans)
{
	currentSum += pRoot->val;
	path.push_back(pRoot->val);

	bool isLeaf = (pRoot->pL_tree == nullptr) && (pRoot->pR_tree == nullptr);
	if (currentSum == expectedSum && isLeaf)
	{
		ans.push_back(path);
	}

	if (pRoot->pL_tree != nullptr)
		FindPath(pRoot->pL_tree, expectedSum, path, currentSum, ans);
	if (pRoot->pR_tree != nullptr)
		FindPath(pRoot->pR_tree, expectedSum, path, currentSum, ans);

	currentSum -= pRoot->val;
	path.pop_back();

}

vector<vector<int>> Get_target(BinaryTree* pRoot, int expectedSum)
{

	std::vector<int> path;
	vector<vector<int>> ans;
	int currentSum = 0;
	FindPath(pRoot, expectedSum, path, currentSum, ans);
	
	return ans;
}

int main()
{
	BinaryTree *root = new BinaryTree(1);
	BinaryTree *l1 = new BinaryTree(2);
	BinaryTree *l1l = new BinaryTree(4);
	BinaryTree *l1r = new BinaryTree(5);
	BinaryTree *r1 = new BinaryTree(3);
	BinaryTree *r1l = new BinaryTree(6);
	BinaryTree *r1r = new BinaryTree(7);

	root->pL_tree = l1;
	root->pR_tree = r1;
	l1->pL_tree = l1l;
	l1->pR_tree = l1r;
	r1->pL_tree = r1l;
	r1->pR_tree = r1r;

	int target = 10;
	cin >> target;
	vector<vector<int>> ans;

	ans = Get_target(root, target);
	if (!ans.empty())
		cout << "Find the target" << endl;
	else
		cout << "Can't Find the targe" << endl;
	return 0;
}

```