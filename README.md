# code-tranning
**输入一个链表，按链表值从尾到头的顺序返回一个ArrayList**

```javascript
function printListFromTailToHead(head)
{
    // write code here
    var arr=[];
    var me=head;
    while(me){
        arr.push(me.val);
        me=me.next;
    }
    return arr.reverse();
}
```

```javascript
function printListFromTailToHead(head)
{
    // write code here
    var arr = []
    while(head !=null) {
        arr.unshift(head.val)
        head = head.next
    }
    return arr
}
```

**请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy**

```javascript
function replaceSpace(str)
{
    return str.replace(/\s/g,'%20')
}
```

**在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。**

利用二维数组由上到下，由左到右递增的规律，
那么选取右上角或者左下角的元素a[row][col]与target进行比较，
当target小于元素a[row][col]时，那么target必定在元素a所在行的左边,
即col--；
当target大于元素a[row][col]时，那么target必定在元素a所在列的下边,
即row++；

```javascript
function Find(target, array)
{
    // write code here
    lenX = array.length;
    lenY = array[0].length;
    for (var i = lenX - 1, j = 0; i >= 0 && j < lenY;) {
        if (target > array[i][j]) {
            j++;
        }
        else if (target < array[i][j]) {
            i--;
        }
        else {
            return true;
        }
    }
    return false
}
```

**输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回**

```javascript
function reConstructBinaryTree(pre, vin)
{
    var len = pre.length;
    return createTree(pre, vin, 0, len - 1, 0);
}
function createTree(pre, vin, left, right, rootIndex){
    var val = pre[rootIndex];
    var midIndex = vin.indexOf(val);
    var root = new TreeNode(val);
    if(midIndex > left) root.left = createTree(pre, vin, left, midIndex - 1, rootIndex + 1 );
    if(midIndex < right) root.right = createTree(pre, vin, midIndex + 1, right, rootIndex + midIndex -left + 1 );
    return root;
}
```

**用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型**

栈A用来作入队列
栈B用来出队列，当栈B为空时，栈A全部出栈到栈B,栈B再出栈（即出队列）

```javascript
var stack1=[],stack2=[];
function push(node)
{
    stack1.push(node);
}
function pop()
{
    if(stack2.length==0){
        if(stack1.length==0){
            return null;
        }else{
            var len = stack1.length;
            for(var i=0;i<len;i++){
                stack2.push(stack1.pop());
            }
            return stack2.pop();
        }
    }else{
        return stack2.pop();
    }
}
```

**把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0**

采用二分法解答这个问题，
mid = low + (high - low)/2
需要考虑三种情况：
(1)array[mid] > array[high]:
出现这种情况的array类似[3,4,5,6,0,1,2]，此时最小数字一定在mid的右边。
low = mid + 1
(2)array[mid] == array[high]:
出现这种情况的array类似 [1,0,1,1,1] 或者[1,1,1,0,1]，此时最小数字不好判断在mid左边
还是右边,这时只好一个一个试 ，
high = high - 1
(3)array[mid] < array[high]:
出现这种情况的array类似[2,2,3,4,5,6,6],此时最小数字一定就是array[mid]或者在mid的左
边。因为右边必然都是递增的。
high = mid
注意这里有个坑：如果待查询的范围最后只剩两个数，那么mid 一定会指向下标靠前的数字
比如 array = [4,6]
array[low] = 4 ;array[mid] = 4 ; array[high] = 6 ;
如果high = mid - 1，就会产生错误， 因此high = mid
但情形(1)中low = mid + 1就不会错误

```javascript
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        int low = 0 ; int high = array.length - 1;   
        while(low < high){
            int mid = low + (high - low) / 2;        
            if(array[mid] > array[high]){
                low = mid + 1;
            }else if(array[mid] == array[high]){
                high = high - 1;
            }else{
                high = mid;
            }   
        }
        return array[low];
    }
}
```

**大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。**

**n<=39**

```javascript
function Fibonacci(n)
{  if(n<=1) {return n;}
   
 else{var f0=0;f1=1
   for(var i=2;i<=n;i++){
        
        f2=f0+f1;
        f0=f1;
        f1=f2;
         
    }
      return f2;}
}
```

**一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）**

对于本题,前提只有 一次 1阶或者2阶的跳法。

a.如果两种跳法，1阶或者2阶，那么假定第一次跳的是一阶，那么剩下的是n-1个台阶，跳法是f(n-1);

b.假定第一次跳的是2阶，那么剩下的是n-2个台阶，跳法是f(n-2)

c.由a\b假设可以得出总跳法为: f(n) = f(n-1) + f(n-2) 

d.然后通过实际的情况可以得出：只有一阶的时候 f(1) = 1 ,只有两阶的时候可以有 f(2) = 2

e.可以发现最终得出的是一个斐波那契数列：

​        

​              | 1, (n=1)

f(n) =     | 2, (n=2)

​              | f(n-1)+f(n-2) ,(n>2,n为整数)

```javascript
public class Solution {
    public int JumpFloor(int target) {
        if (target <= 0) {
            return -1;
        } else if (target == 1) {
            return 1;
        } else if (target ==2) {
            return 2;
        } else {
            return  JumpFloor(target-1)+JumpFloor(target-2);
        }
    }
}

```

**一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法**

关于本题，前提是n个台阶会有一次n阶的跳法。分析如下:

f(1) = 1

f(2) = f(2-1) + f(2-2)         //f(2-2) 表示2阶一次跳2阶的次数。

f(3) = f(3-1) + f(3-2) + f(3-3) 

...

f(n) = f(n-1) + f(n-2) + f(n-3) + ... + f(n-(n-1)) + f(n-n) 

 

说明： 

1）这里的f(n) 代表的是n个台阶有一次1,2,...n阶的 跳法数。

2）n = 1时，只有1种跳法，f(1) = 1

3) n = 2时，会有两个跳得方式，一次1阶或者2阶，这回归到了问题（1） ，f(2) = f(2-1) + f(2-2) 

4) n = 3时，会有三种跳得方式，1阶、2阶、3阶，

​    那么就是第一次跳出1阶后面剩下：f(3-1);第一次跳出2阶，剩下f(3-2)；第一次3阶，那么剩下f(3-3)

​    因此结论是f(3) = f(3-1)+f(3-2)+f(3-3)

5) n = n时，会有n中跳的方式，1阶、2阶...n阶，得出结论：

​    f(n) = f(n-1)+f(n-2)+...+f(n-(n-1)) + f(n-n) => f(0) + f(1) + f(2) + f(3) + ... + f(n-1)

​    

6) 由以上已经是一种结论，但是为了简单，我们可以继续简化：

​    f(n-1) = f(0) + f(1)+f(2)+f(3) + ... + f((n-1)-1) = f(0) + f(1) + f(2) + f(3) + ... + f(n-2)

​    f(n) = f(0) + f(1) + f(2) + f(3) + ... + f(n-2) + f(n-1) = f(n-1) + f(n-1)

​    可以得出：

​    f(n) = 2*f(n-1)

​    

7) 得出最终结论,在n阶台阶，一次有1、2、...n阶的跳的方式时，总得跳法为：

​              | 1       ,(n=0 ) 

f(n) =     | 1       ,(n=1 )

​              | 2*f(n-1),(n>=2)

```javascript
public class Solution {
    public int JumpFloorII(int target) {
        if (target <= 0) {
            return -1;
        } else if (target == 1) {
            return 1;
        } else {
            return 2 * JumpFloorII(target - 1);
        }
    }
}

```

**我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？**

**思路分析：**

痛定思痛，还是不能够贪小便宜。用归纳法归纳如下，

（1）当 n < 1时，显然不需要用2*1块覆盖，按照题目提示应该返回 0。

（2）当 n = 1时，只存在一种情况。

![img](https://uploadfiles.nowcoder.com/images/20160821/610669_1471715163771_7D5D4E0729A4FC3E473AD660E13B782E) 

（3）当 n = 2时，存在两种情况。

![img](https://uploadfiles.nowcoder.com/images/20160821/610669_1471715305312_F22B8EBDEC046FD7D7D93725B669BF33) 

（4）当 n = 3时，明显感觉到如果没有章法，思维难度比之前提升挺多的。

![img](https://uploadfiles.nowcoder.com/images/20160821/610669_1471715340361_4A8CA1EA1EFD2C46E73DB31C97F30D48) 

... 尝试归纳，本质上 n 覆盖方法种类都是对 n - 1 时的扩展。

可以明确，n 时必定有 n-1时原来方式与2*1的方块结合。也就是说, f(n) = f(n-1) + ?(暂时无法判断)。

（4）如果我们现在归纳 n = 4，应该是什么形式？

4.1）保持原来n = 3时内容，并扩展一个 2*1 方块，形式分别为 “| | | |”、“= | |”、“| = |”

4.2）新增加的2*1 方块与临近的2*1方块组成 2*2结构，然后可以变形成 “=”。于是 n = 4在原来n = 3基础上增加了"| | ="、“= =”。

再自己看看这多出来的两种形式，是不是只比n = 2多了“=”。其实这就是关键点所在...因为，只要2*1或1*2有相同的两个时，就会组成2*2形式，于是就又可以变形了。

所以，自然而然可以得出规律： f(n) = f(n-1) + f(n-2)， (n > 2)。

如果看了这一套理论还存在疑惑。可以尝试将题目改成1*3方块覆盖3*n、1*4方块覆盖4*n。

相应的结论应该是：

（1）1 * 3方块 覆 盖3*n区域：f(n) = f(n-1) + f(n - 3)， (n > 3)

（2） 1 *4 方块 覆 盖4*n区域：f(n) = f(n-1) + f(n - 4)，(n > 4)

更一般的结论，如果用1*m的方块覆盖m*n区域，递推关系式为f(n) = f(n-1) + f(n-m)，(n > m)

```javascript
public class Solution {
    public int JumpFloorII(int target) {
        if (target <= 0) {
            return -1;
        } else if (target == 1) {
            return 1;
        } else {
            return 2 * JumpFloorII(target - 1);
        }
    }
}

```

**输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示**

如果一个整数不为0，那么这个整数至少有一位是1。如果我们把这个整数减1，那么原来处在整数最右边的1就会变为0，原来在1后面的所有的0都会变成1(如果最右边的1后面还有0的话)。其余所有位将不会受到影响。
举个例子：一个二进制数1100，从右边数起第三位是处于最右边的一个1。减去1后，第三位变成0，它后面的两位0变成了1，而前面的1保持不变，因此得到的结果是1011.我们发现减1的结果是把最右边的一个1开始的所有位都取反了。这个时候如果我们再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。如1100&1011=1000.也就是说，把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。

```javascript
public class Solution {
    public int NumberOf1(int n) {
        int count = 0;
        while(n!= 0){
            count++;
            n = n & (n - 1);
         }
        return count;
    }
}

```

**给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。**

  本方法思想：如果求10次方用循环做，需要做十次，但是如果我们求5次方的2次方只需要五次即可，9次方=4次方*4次方*本身，所以这就使得我们想到用递归求解，同时要注意负数和0的问题。

![img](https://uploadfiles.nowcoder.com/images/20170907/3270776_1504748011304_B16239181123036ECE974C89CC410F1F)![img](https://uploadfiles.nowcoder.com/files/20170906/3270776_1504711188579_E695B0E580BCE79A84E695B4E695B0E6ACA1E696B9.png)

```javascript
function Power(x,n){
    if(n < 0) {
        if(x <= 0) {
            throw new Error("分母不能小于等于0");
        }else {
            if(-n % 2 == 1) {
                return 1/(Power(x,-n-1) * x);
            }else {
                var r = 1/Power(x,-n/2);
            return r * r;
            }
        }
    }
    if(n == 0) {
        return 1;
    }
    else {
        if(n % 2 == 1) {
            return Power(x,n-1) * x;
        }else {
            var r = Power(x,n/2);
            return r * r;
        }
    }
    
}
```

**输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。**

```javascript
function reOrderArray(array)
{
    // write code here
    var arr1=[],arr2=[];
    for(var i=0;i<array.length;i++){
        if(array[i]%2!=0){
            arr1.push(array[i]);
        }
        else{
            arr2.push(array[i]);
        }
    }
    return arr1.concat(arr2);
}
```

**输入一个链表，输出该链表中倒数第k个结点。**

```javascript
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindKthToTail(head, k)
{
    var arr = [];
    while(head!=null){
        arr.push(head);
        head = head.next;
    }
    return arr[arr.length-k];
}
```

**输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。**

```javascript
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function Merge(pHead1, pHead2)
{
    // write code here
    let list = {}
    if(pHead1 === null){
        return pHead2;
    } else if (pHead2 === null) {
        return pHead1;
    }
    if(pHead1 > pHead2){
        list = pHead2;
        list.next = Merge(pHead2.next, pHead1);
    } else {
        list = pHead1;
        list.next = Merge(pHead2, pHead1.next)
    }
    return list;
}
```

**输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）**

```javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function isSubtree(root1, root2) {
    if (root2 == null) return true;
    if (root1 == null) return false;
    if (root1.val == root2.val) {
        return isSubtree(root1.left, root2.left)
            && isSubtree(root1.right, root2.right);
    } else {
        return false; 
    }
}
  
function HasSubtree(pRoot1, pRoot2)
{
   if (pRoot1 == null || pRoot2 == null) {
       return false;
   }
    return isSubtree(pRoot1, pRoot2)
        || HasSubtree(pRoot1.left, pRoot2)
        || HasSubtree(pRoot1.right, pRoot2);
}
```

**操作给定的二叉树，将其变换为源二叉树的镜像。**

```javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function Mirror(root)
{
    // write code here
    if(root === null) {
        return;
    }
    var temp = root.left;
    root.left = root.right;
    root.right = temp;
    Mirror(root.left);
    Mirror(root.right);
}
```

**定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。**

思路：用一个栈data保存数据，用另外一个栈min保存依次入栈最小的数
比如，data中依次入栈，5,  4,  3, 8, 10, 11, 12, 1
       则min依次入栈，5,  4,  3，no,no, no, no, 1

no代表此次不如栈
每次入栈的时候，如果入栈的元素比min中的栈顶元素小或等于则入栈，否则不如栈。

```javascript
var stackData = [];
var stackMin = [];
function push(node)
{
    stackData.push(node);
    if (stackMin.length ===0 || node <= stackMin[stackMin.length - 1]) {
        stackMin.push(node);
        return;
    }
}
function pop()
{
    if (stackData.length === 0) {
        throw new Error('Your stack is empty!');
    } 
    var result = stackData.pop();
    if (result === stackMin[stackMin.length - 1]) {
        stackMin.pop();
    }
    // write code here
}
function top()
{
    return stackData[stackData.length - 1];
    // write code here
}
function min()
{
    if (stackData.length === 0) {
        throw new Error('Your stack is empty!');
    } 
    return stackMin[stackMin.length - 1];
    // write code here
}
```

**把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。**

  首先从题目可以知道，对于一个丑数p，p*2、p*3、p*5都是丑数。

那么从第一个丑数1开始，1*2、1*3、1*5都是丑数，最小的2是第二个丑数；

对于第二个丑数2来说，又多出来三个需要被比较的数字，即2*2、2*3、2*5，再加上第一轮挑剩下的1*3、1*5，但是这里显然可以看出来，1*3<2*3，1*5<2*5，所以其实只需要比较2*2、1*3、1*5即可。<br>
......

按照这样的节奏比下去即可。  



说下思路，如果p是丑数，那么p=2^x * 3^y * 5^z
那么只要赋予x,y,z不同的值就能得到不同的丑数。
如果要顺序找出丑数，要知道下面几个特（fei）点（hua）。
对于任何丑数p：
（一）那么2*p,3*p,5*p都是丑数，并且2*p<3*p<5*p
（二）如果p<q, 那么2*p<2*q,3*p<3*q,5*p<5*q
现在说说算法思想：
    由于1是最小的丑数，那么从1开始，把2*1，3*1，5*1，进行比较，得出最小的就是1
的下一个丑数，也就是2*1，
    这个时候，多了一个丑数‘2’，也就又多了3个可以比较的丑数，2*2，3*2，5*2，
这个时候就把之前‘1’生成的丑数和‘2’生成的丑数加进来也就是
(3*1,5*1,2*2，3*2，5*2)进行比较，找出最小的。。。。如此循环下去就会发现，
每次选进来一个丑数，该丑数又会生成3个新的丑数进行比较。
    上面的暴力方法也应该能解决，但是如果在面试官用这种方法，估计面试官只会摇头吧
。下面说一个O（n）的算法。
    在上面的特（fei）点（hua）中，既然有p<q, 那么2*p<2*q，那么
“我”在前面比你小的数都没被选上，你后面生成新的丑数一定比“我”大吧，那么你乘2
生成的丑数一定比我乘2的大吧，那么在我选上之后你才有机会选上。
其实每次我们只用比较3个数：用于乘2的最小的数、用于乘3的最小的数，用于乘5的最小的
数。也就是比较(2*x , 3*y, 5*z) ，x>=y>=z的，
重点说说下面代码中p的作用：int p[] = new int[] { 0, 0, 0 }; p[0]表示最小用于
乘2比较数在数组a中的【位置】。 

```javascript
function GetUglyNumber_Solution(index)
{
    if(index == 0){
        return 0;
    }
    var uglyArr = [1],
        two = 0,
        three = 0,
        five = 0;
    for(var i=1;i<index;i++){
        uglyArr[i] = Math.min(uglyArr[two]*2,uglyArr[three]*3,uglyArr[five]*5);
        if(uglyArr[i]==uglyArr[two]*2){
            two++;
        }
        if(uglyArr[i]==uglyArr[three]*3){
            three++;
        }
        if(uglyArr[i]==uglyArr[five]*5){
            five++;
        }
    }
    return uglyArr[index-1];
}
```

**输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。**

对vector容器内的数据进行排序，按照 将a和b转为string后
 若 a＋b<b+a  a排在在前 的规则排序,
 如 2 21 因为 212 < 221 所以 排序后为 21 2 
  to_string() 可以将int 转化为string

```javascript
function PrintMinNumber(numbers)
{
    // write code here
    numbers.sort(compare);
    var result = "";
    for(var i = 0; i < numbers.length; i++){
        result += numbers[i];
    }
    return result;
     
}
 
function compare(a, b){
    var str1 = a + "" + b;
    var str2 = b + "" + a;
    for(var i = 0; i < str1.length; i++){
        if(str1.charAt(i) > str2.charAt(i)){
            return 1;
        }
        if(str1.charAt(i) < str2.charAt(i)){
            return -1;
        }
    }
    return 1;
}
```

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

```javascript
function GetLeastNumbers_Solution(input, k)
{
    var result = input.sort(function(a,b){
        return a-b;
    });
    return result.length>=k?result.slice(0,k):[];
}
```

**输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。**

```javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function Convert(pRootOfTree)
{
    // write code here
    if(!pRootOfTree)
        return null;
    var arr=[],len=0;
    sub(pRootOfTree,arr);
    len=arr.length;
    arr[0].left=null;
    arr[0].right=arr[1];
    for(var i=1;i<len-1;i++){
        arr[i].left=arr[i-1];
        arr[i].right=arr[i+1];
    }
    arr[len-1].left=arr[len-2];
    arr[len-1].right=null;
    return arr[0];
}
function sub(node,arr){
    if(!node)
        return;
    sub(node.left,arr);
    arr.push(node);
    sub(node.right,arr);
}
```

**HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)**

<https://blog.csdn.net/iteye_11788/article/details/82550236>

**输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。**

<https://www.cnblogs.com/cxjchen/p/3932949.html>

正常人的思维是，固定第一个字符，然后依次将后面的字符串与前面的交换，那么排列的个数就是除了第一个字符以外，其他字符的排列个数+1。

也就是固定一个字符串之后，之后再将问题变小，只需求出后面子串的排列个数就可以得出结果，当然第一时间想到的就是递归的算法了。

下面这张图很清楚的给出了递归的过程：

很明显，递归的出口，就是只剩一个字符的时候，递归的循环过程，就是从每个子串的第二个字符开始依次与第一个字符交换，然后继续处理子串。

还有一个问题要注意，就是如果字符串中有重复的字符串

由于全排列就是从第一个数字起，每个数分别与它后面的数字交换，我们先尝试加个这样的判断——如果一个数与后面的数字相同那么这两个数就不交换 了。例如abb，第一个数与后面两个数交换得bab，bba。然后abb中第二个数和第三个数相同，就不用交换了。但是对bab，第二个数和第三个数不 同，则需要交换，得到bba。由于这里的bba和开始第一个数与第三个数交换的结果相同了，因此这个方法不行。

换种思维，对abb，第一个数a与第二个数b交换得到bab，然后考虑第一个数与第三个数交换，此时由于第三个数等于第二个数，所以第一个数就不再用与第三个数交换了。再考虑bab，它的第二个数与第三个数交换可以解决bba。此时全排列生成完毕！



这样，我们得到在全排列中去掉重复的规则：

去重的全排列就是从第一个数字起，每个数分别与它后面非重复出现的数字交换。

 ```c
#include <stdio.h>

static int count = 0;

void swap(char* str,int a,int b)
{
    char tmp = str[a];
    str[a] = str[b];
    str[b] = tmp;
}


int is_swap(char *str, int begin, int k){   //判断从子串的第一个字符串开始，直到k-1位置，看是否有重复的字符
    int i, flag;

    for (i = begin, flag = 1; i < k; i ++) {
        if (str[i] == str[k]) {
            flag = 0;
            break;
        }
    }

    return flag;
}

void full_permutation(char* str,int begin,int end)
{
    if (begin == end)
    {
        count++;//此处可以输出字符串或者记录字符串
        return;
    }else{
        int i;
        for (i = begin; i <= end; i++)
        {
            if (is_swap(str,begin,i))
            {
                swap(str,begin,i);
                full_permutation(str,begin+1,end);
                swap(str,begin,i);
            }
        }
    }
}

int main()
{
    char str[7] = {'a','l','i','b','a','b','a'};
    full_permutation(str,0,6);
    printf("count=%d",count);
    return 0;
}
 ```

```javascript
var result = [];
function Permutation(str){
    result = []
    if(str.length<=0) return result;
    var sortTmp = "";
    var arr = str.split("");
    result = sortString(arr,sortTmp)
    return result;
}
 
function sortString(arr,sortTmp){
    if(arr.length ==0 ){
        result.push(sortTmp);
    }else{
        var isRepeated = {}
        for(var i = 0; i<arr.length; i++){
            if(!isRepeated[arr[i]]){
                var p = arr.splice(i,1)[0];
                sortTmp += p;
                sortString(arr,sortTmp);
                arr.splice(i,0,p); //恢复字符串
                sortTmp = sortTmp.slice(0,sortTmp.length-1);
                isRepeated[p] = true;
            }
        }
    }
    return result;
}
```

**一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。**

```javascript
function FindNumsAppearOnce(array)
{
    // write code here
    // return list, 比如[a,b]，其中ab是出现一次的两个数字
    var arr = [];
    for(var i = 0; i < array.length; i++) {
        if(array.indexOf(array[i]) === array.lastIndexOf(array[i])) {
            arr.push(array[i]);
        }
    }
    return arr;
}
```

**输入一棵二叉树，判断该二叉树是否是平衡二叉树。**

```javascript
function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
}
var isBalanced = true;
function IsBalanced_Solution(pRoot){
    if(pRoot == null){
        return true;
    }
    IsBalanced(pRoot);
    var result = isBalanced;
    isBalanced = true;
    return result;
}
function IsBalanced(pRoot){
    if(pRoot == null){
        return 0;
    }
    var left = 0,
        right = 0;
    if(pRoot.left){
        left = IsBalanced(pRoot.left);
    }
    if(pRoot.right){
        right = IsBalanced(pRoot.right);
    }
    if(Math.abs(left - right) > 1){
        isBalanced = false;
    }
    return left > right ? left + 1 : right + 1;
}
```

**统计一个数字在排序数组中出现的次数。**

```javascript
function GetNumberOfK(data, k)
{
    var count = 0;
    var idx = data.indexOf(k);
    while(data[idx]==k){
        count++;
        idx++;
    }
    return count;
}
```

**输入两个链表，找出它们的第一个公共结点。**

```javascript
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindFirstCommonNode(pHead1, pHead2)
{
    var p1=pHead1;
    var p2=pHead2;
    while(p1!=p2){
        p1=p1==null?pHead2:p1.next;
        p2=p2==null?pHead1:p2.next;
    }
    return p1;
}
```

**每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)**

如果只求最后一个报数胜利者的话，我们可以用数学归纳法解决该问题，为了讨      论方便，先把问题稍微改变一下，并不影响原意：

 问题描述：n个人（编号0~(n-1))，从0开始报数，报到(m-1)的退出，剩下的人 继续从0开始报数。求胜利者的编号。

 我们知道第一个人(编号一定是m%n-1) 出列之后，剩下的n-1个人组成了一个新      的约瑟夫环（以编号为k=m%n的人开始）:

        k  k+1  k+2  ... n-2, n-1, 0, 1, 2, ... k-2并且从k开始报0。

现在我们把他们的编号做一下转换：

k     --> 0

k+1   --> 1

k+2   --> 2

...

...

k-2   --> n-2

k-1   --> n-1

变换后就完完全全成为了(n-1)个人报数的子问题，假如我们知道这个子问题的解： 例如x是最终的胜利者，那么根据上面这个表把这个x变回去不刚好就是n个人情 况的解吗？！！变回去的公式很简单，相信大家都可以推出来：x'=(x+k)%n。

令f[i]表示i个人玩游戏报m退出最后胜利者的编号，最后的结果自然是f[n]。

递推公式

f[1]=0;

f[i]=(f[i-1]+m)%i;  (i>1)

有了这个公式，我们要做的就是从1-n顺序算出f[i]的数值，最后结果是f[n]。 因为实际生活中编号总是从1开始，我们输出f[n]+1。

```javascript
function LastRemaining_Solution(n, m)
{
    // write code here
    if(n == 0){
        return -1;
    }
    if(n == 1){
        return 0;
    }else{
        return (LastRemaining_Solution(n - 1, m) + m) % n;
    }
     
}
```

**LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何， 如果牌能组成顺子就输出true，否则就输出false。为了方便起见,你可以认为大小王是0。**

思路：

1）没有大小王的时候即判断数是否连续；

2）有大小王的时候，判断数的间隔是否小于王的数量。小于返回true，大于返回false；

3）有相等的牌则直接返回false。

```java
import java.util.*;
public class Solution {
    public boolean isContinuous(int [] numbers) {
        if(numbers == null || numbers.length <= 4)
            return false;
         
        //先排序，否则计算间隔的时候可能会出现负值，比较麻烦
        Arrays.sort(numbers);
        int totalGap = 0;
        //计算大小王的数量
        int countZero = 0;
        for(int i = 0; i < numbers.length; i++){
            if(numbers[i] == 0){
                countZero++;
                continue;
            }
            //计算两数之间的间隔
            if(i < numbers.length - 1){
                int gap = numbers[i + 1] - numbers[i] - 1;
                //如果出现对子，如2 2，则gap为-1，直接返回false
                if(gap < 0)
                    return false;
                totalGap += gap;
            }
        }
        //所有数间隔大于王数量，就返回false
        if(totalGap > countZero){
            return false;
        }
        return true;
    }
}
```

**牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？**

```javascript
function ReverseSentence(str)
{
    return str.split(" ").reverse().join(" ");
}
```

**汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！**

```javascript
function LeftRotateString(str, n)
{
    if(str==null||str.length==0){
        return "";
    }
    n=n%str.length;
    return str.slice(n)+str.slice(0,n);   
}
```

**输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。**

数列满足递增，设两个头尾两个指针i和j，

若ai + aj == sum，就是答案（相差越远乘积越小）

若ai + aj > sum，aj肯定不是答案之一（前面已得出 i 前面的数已是不可能），j -= 1

若ai + aj < sum，ai肯定不是答案之一（前面已得出 j 后面的数已是不可能），i += 1

```java
typedef vector<int> vi;
class Solution {
public:
    vi FindNumbersWithSum(const vi& a,int sum) {
        vi res;
        int n = a.size();
        int i = 0, j = n - 1;
        while(i < j){
            if(a[i] + a[j] == sum){
                res.push_back(a[i]);
                res.push_back(a[j]);
                break;
            }
            while(i < j && a[i] + a[j] > sum) --j;
            while(i < j && a[i] + a[j] < sum) ++i;
        }
        return res;
    }
};
```

**小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!**

在答案区找到一个答案，说的很好，叫做双指针技术，就是相当于有一个窗口，窗口的左右两边就是两个指针，我们根据窗口内值之和来确定窗口的位置和宽度。非常牛逼的思路，虽然双指针或者所谓的滑动窗口技巧还是蛮常见的，但是这一题还真想不到这个思路。

```javascript
import java.util.ArrayList;
public class Solution {
    public ArrayList<ArrayList<Integer> > FindContinuousSequence(int sum) {
        //存放结果
        ArrayList<ArrayList<Integer> > result = new ArrayList<>();
        //两个起点，相当于动态窗口的两边，根据其窗口内的值的和来确定窗口的位置和大小
        int plow = 1,phigh = 2;
        while(phigh > plow){
            //由于是连续的，差为1的一个序列，那么求和公式是(a0+an)*n/2
            int cur = (phigh + plow) * (phigh - plow + 1) / 2;
            //相等，那么就将窗口范围的所有数添加进结果集
            if(cur == sum){
                ArrayList<Integer> list = new ArrayList<>();
                for(int i=plow;i<=phigh;i++){
                    list.add(i);
                }
                result.add(list);
                plow++;
            //如果当前窗口内的值之和小于sum，那么右边窗口右移一下
            }else if(cur < sum){
                phigh++;
            }else{
            //如果当前窗口内的值之和大于sum，那么左边窗口右移一下
                plow++;
            }
        }
        return result;
    }
}
```

