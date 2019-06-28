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

