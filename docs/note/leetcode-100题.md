### leetcode 热题100题

#### 538. [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

![](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200412162506.png)

代码思路：反序中序遍历的方法

>  BST的中序遍历就是从小到大,那么反过来就是从大到小,然后累加就好了.

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
    int num=0;
public:
    TreeNode* convertBST(TreeNode* root) {
        if(root!=NULL){
            //遍历右子树
            convertBST(root->right);
            //遍历节点
            root->val=root->val+num;
            num=root->val;
            //遍历左子树
            convertBST(root->left);
            return root;
        }
        return NULL;
    }
};
```

时间复杂度：O(n)

空间复杂度：O(n)

- [ ] 是否独立解答
- [x] 是否理解程序代码

---

#### [448. 找到所有数组中消失的数字](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

> 您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

> 输入:
> [4,3,2,7,8,2,3,1]
>
> 输出:
> [5,6]

我的代码：

> 先排序，然后判断相邻两位的差值是否大于1，大于1则证明中间缺少数字，数组首尾是否为1和n单独判断

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        if(nums.size()<1) return nums;
        sort(nums.begin(),nums.end());
        int len=nums.size();
        vector<int> n;

        if(nums[0]!=1){
            int j=nums[0]-1;
            for(int k=1;k<=j;k++){
                    n.push_back(k);
                }
        }

        for(int i=0;i<len-1;i++){
            if(nums[i+1]-nums[i]>1){
                int j=nums[i+1]-nums[i];
                for(int k=1;k<j;k++){
                    n.push_back(nums[i]+k);
                }
            }
        }
        if(nums[len-1]!=len){
            int j=len-nums[len-1];
            for(int k=1;k<=j;k++){
                    n.push_back(nums[len-1]+k);
                }
        }
        return n;
    }
};
```

> 执行用时 :228 ms, 在所有 C++ 提交中击败了6.32%的用户
>
> 内存消耗 :32.4 MB, 在所有 C++ 提交中击败了5.56%的用户

时间复杂度：O(n^2)

空间复杂度：O(n)

- [x] 是否独立完成
- [x] 是否理解代码

**优秀解答：**

>将所有正数作为*数组下标*，置对应数组值为负值。那么，仍为正数的位置即为（未出现过）消失的数字。

![image-20200412170955971](https://gitee.com/qiaoyukeji/markdown_tupian/raw/master/markdown/20200412170958.png)

```c++
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        for (int i = 0; i < nums.size(); ++i)
        nums[abs(nums[i])-1] = -abs(nums[abs(nums[i])-1]);
        vector<int> res;
        for (int i = 0; i < nums.size(); ++i){
            if (nums[i] > 0)
                res.push_back(i+1);
        }
        return res;
        }
};
```

> 执行用时 :112 ms, 在所有 C++ 提交中击败了37.58%的用户
>
> 内存消耗 :32.2 MB, 在所有 C++ 提交中击败了5.56%的用户

- [x]  代码是否理解

时间复杂度：O(n)

空间复杂度：O(n)

---

#### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表**：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

 我的代码：

> 首先计算出两链表的长度差 len，让长链表指针先走 len，然后两链表指针一起走，当两链表指针指到同一位置时，即找到相交点。



```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 * };
 */
class Solution {
    int a=0,b=0;
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* pA=headA;
        ListNode* pB=headB;
        while(pA!=NULL){
            a++;
            pA=pA->next;
        }
        while(pB!=NULL){
            b++;
            pB=pB->next;
        }
        pA=headA;
        pB=headB;
        if(a>=b){
            int len=a-b;
            while(len--){
                pA=pA->next;
            }
            while(b--){
                if(pB==pA){
                    return pA;
                }
                pA=pA->next;
                pB=pB->next;
            }
            return NULL;
        }
        if(a<b){
            int len=b-a;
            while(len--){
                pB=pB->next;
            }
            while(a--){
                if(pB==pA){
                    return pA;
                }
                pA=pA->next;
                pB=pB->next;
            }
            return NULL;
        }
 	return NULL;
    }
};
```

> 执行用时 :60 ms, 在所有 C++ 提交中击败了56.78%的用户
>
> 内存消耗 :14.7 MB, 在所有 C++ 提交中击败了100.00%的用户

- [x]  是否独立完成
- [x] 是否理解代码

时间复杂度：O(n)

空间复杂度：O(1)



---

#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你**最多**只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

##### 暴力模式：

> 我们需要找出给定数组中两个数字之间的最大差值（即，最大利润）。此外，第二个数字（卖出价格）必须大于第一个数字（买入价格）。

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = (int)prices.size(), ans = 0;
        for (int i = 0; i < n; ++i){
            for (int j = i + 1; j < n; ++j){
                ans = max(ans, prices[j] - prices[i]);
            }
        }
        return ans;
    }
};
```

> 执行超时。

- [ ]   是否独立完成
- [x]  是否理解代码

时间复杂度：O(n^2)

空间复杂度：O(1)



##### 利用栈:

[相关链接](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/c-li-yong-shao-bing-wei-hu-yi-ge-dan-diao-zhan-tu-/#comment)

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ans = 0;
        vector<int> St;
        prices.emplace_back(-1); // 哨兵👨‍✈️,运行到最后一个(哨兵)时，强制当前栈顶出栈并计算利润(与栈底元素差值)
        for (int i = 0; i < prices.size(); ++ i){
            while (!St.empty() && St.back() > prices[i]){ // 当栈不为空时或栈顶元素大于即将要入栈元素时，计算栈顶与栈底元素差
                ans = std::max(ans, St.back() - St.front()); // 计算栈顶与栈底元素差,并维护最大值
                St.pop_back();//栈顶元素出栈
            }
            St.emplace_back(prices[i]);//否则将要入栈的元素入栈
        }

        return ans;
    }
};

```

> 执行用时 :16 ms, 在所有 C++ 提交中击败了32.69%的用户
>
> 内存消耗 :13.3 MB, 在所有 C++ 提交中击败了5.19%的用户

- [ ]    是否独立完成
- [x]   是否理解代码

#### [155. 最小栈](https://leetcode-cn.com/problems/min-stack/)

设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) —— 将元素 x 推入栈中。
pop() —— 删除栈顶的元素。
top() —— 获取栈顶元素。
getMin() —— 检索栈中的最小元素。

示例:

```cpp
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```



思路：

>  思路：每次入栈2个元素，一个是入栈的元素本身，一个是当前栈元素的最小值 * 如：入栈序列为2-3-1，则入栈后栈中元素序列为：2-2-3-2-1-1 * 用空间代价来换取时间代价

```c++
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        if(st.empty()){
            st.push(x);
            st.push(x);
        }else{
            int tmp=st.top();
            st.push(x);
            if(tmp<x){
                st.push(tmp);
            }else{
                st.push(x);
            }
        }

    }
    
    void pop() {
        st.pop();
        st.pop();
    }
    
    int top() {
        int t=st.top();
        st.pop();
        int top=st.top();
        st.push(t);
        return top;
    }
    
    int getMin() {
        return st.top();
    }
    private:
    stack<int> st;
    
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

>  执行用时 :44 ms, 在所有 C++ 提交中击败了43.73%的用户
>
> 内存消耗 :15 MB, 在所有 C++ 提交中击败了100.00%的用户

- [ ] 是否独立完成
- [x] 是否理解代码



[官方题解](https://leetcode-cn.com/problems/min-stack/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-38/)：

> 这道题最直接的解法就是我们可以用两个栈，一个栈去保存正常的入栈出栈的值，另一个栈去存最小值，也就是用栈顶保存当前所有元素的最小值。存最小值的栈的具体操作流程如下：
>
> 将第一个元素入栈。
>
> 新加入的元素如果大于栈顶元素，那么新加入的元素就不处理。
>
> 新加入的元素如果小于等于栈顶元素，那么就将新元素入栈。
>
> 出栈元素不等于栈顶元素，不操作。
>
> 出栈元素等于栈顶元素，那么就将栈顶元素出栈。
>

```c++
class MinStack {
    /** initialize your data structure here. */
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        if (!minStack.isEmpty()) {
            int top = minStack.peek();
            //小于的时候才入栈
            if (x <= top) {
                minStack.push(x);
            }
        }else{
            minStack.push(x);
        }
    }

    public void pop() {
        int pop = stack.pop();

        int top = minStack.peek();
        //等于的时候再出栈
        if (pop == top) {
            minStack.pop();
        }

    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

- [ ] 是否独立完成
- [x] 是否理解代码

---

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：

> 输入： 2
> 输出： 2
> 解释： 有两种方法可以爬到楼顶。
>
> > 
> > 1.  1 阶 + 1 阶
> > 2.  2 阶
> > 

解题思路：使用递归来做，第n阶台阶需要n-1阶台阶+1，或者n-2阶台阶+2.

```c++
class Solution {
public:
    int climbStairs(int n) {
        if(n==1) return 1;
        if(n==2) return 2;
        return climbStairs(n-1)+climbStairs(n-2);
        
    }
};
```

当n=44时，报超时。**21 / 45** 个通过测试用例。

时间复杂度：O(2^n)

空间复杂度：O(n)

- [x] 是否独立完成
- [x] 是否理解代码



解题思路：循环方式从1开始，n=(n-1)+(n-2)

```c++
class Solution {
public:
    int climbStairs(int n) {
        if(n==1) return 1;
        if(n==2) return 2;
        int sum=0,j=1,k=2;
        for(int i=3;i<=n;i++){
            sum=j+k;
            j=k;
            k=sum;
        }
        return sum;   
    }
};
```

执行用时 :0 ms, 在所有 C++ 提交中击败了100.00%的用户

内存消耗 :6 MB, 在所有 C++ 提交中击败了100.00%的用户

时间复杂度：O(n)

空间复杂度：O(1)

- [x] 是否独立完成
- [x]  是否理解代码

---

#### [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。

示例 1:

> 输入: [1,2,3,1]
> 输出: 4
> 解释: 偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
>      偷窃到的最高金额 = 1 + 3 = 4 。

解题思路：动态规划，`dp[i]=max(dp[i-2]+nums[i]，dp[i-1])`

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0) return 0;
        int dp[nums.size()];
        dp[0]=nums[0];
        for(int i=1;i<nums.size();i++){
            if(i==1){dp[i]= max(nums[0],nums[1]);}
            else{
                dp[i]=max(dp[i-2]+nums[i],dp[i-1]);
            }
        }
        return dp[nums.size()-1];


    }
};
```

执行用时 :4 ms, 在所有 C++ 提交中击败了58.08%的用户

内存消耗 :7.8 MB, 在所有 C++ 提交中击败了100.00%的用户

时间复杂度：O(n)

空间复杂度：O(n)

- [ ] 是否独立完成
- [ ]  是否理解代码

---

