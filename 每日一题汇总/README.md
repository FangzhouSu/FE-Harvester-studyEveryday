# [22/1/12每日一题](https://github.com/FangzhouSu/FE-Harvester-studyEveryday/issues/1)

> 更多内容戳[标题](https://github.com/FangzhouSu/FE-Harvester-studyEveryday/issues/1)见讨论区嗷！

> 1、CSS篇：定位中，absolute 与 fixed 共同点与不同点
> 2、JavaScript篇：闭包的概念及特点
> 3、算法：说一下递归和迭代的区别是什么，各有什么优缺点？
> 4、力扣101.对称二叉树：给你一个二叉树的根节点root，检查它是否轴对称。

## 1、CSS篇：定位中，absolute 与 fixed 共同点与不同点

共同点：

- 改变行内元素的呈现方式，将 display 置为 `inline-block`

- 使元素**脱离普通文档流**，不再占据文档物理空间，**触发BFC**

- **覆盖非定位文档元素**

不同点：

- absolute 与 fixed 的**根元素**不同，absolute 的根元素可以设置，fixed 根元素是浏览器。

- 在有滚动条的页面中，absolute 会跟着父元素进行移动，fixed 固定在页面的具体位置。
- absolute是相对于离它最近的有相对定位的父元素进行定位（一般使用子绝父相，如果没有定位的父元素则相对于浏览器窗口）；fixed是相对于浏览器窗口定位。



## 2、JavaScript篇：闭包的概念及特点

> 闭包的知识点有很多有趣的点！这里建议多看一些**[例子](https://github.com/FangzhouSu/FE-Harvester-studyEveryday/issues/1)**学习一下，但也别太纠结！

> [相关讨论](https://github.com/FangzhouSu/FE-Harvester-studyEveryday/issues/1#issuecomment-1010670778)

- 1、概念

【1】闭包函数：声明在一个函数中的函数，叫做闭包函数，闭包函数可以访问其他函数内部变量。

【2】内部函数引用外部函数的数据，并且**外部函数执行就会产生闭包**。

【3】闭包：内部函数**总是可以访问其所在的外部函数中声明的参数和变量**，即使在其外部函数被返回（寿命终结）了之后。利用闭包可以**突破作用域链**。



【4】使用闭包一般是为了**设计私有的方法和属性**。

- 2、特点（优点）

  - 让**外部访问函数内部变量**成为可能；
  - 可以避免使用全局变量，**防止全局变量污染**；

- 3、缺点

  - 【1】可能导致*内存溢出*（面试高频）

  ```js
  var obj = {};
  for(var i = 0; i < 10000; i++){
      obj[i] = new Array(1000000);// new Array(1000000)定义一个长度为1000000的数组
      console.log('------')
  }// 这个代码会导致内存溢出 浏览器会做一个崩溃的设置 终止程序
  ```

  内存溢出是指存储的数据超出了指定空间的大小，这时数据就会越界

  - 【2】可能会导致*内存泄露*

  ```js
  function fn1(){
      var arr = new Array[10000000]
      function fn2(){
          console.log(arr.length);
      }
      return fn2;
  }
  var f = fn1();
  f();// fn1形成闭包 本该释放的arr变量现在不会被释放！
  ```

  **内存泄漏**的意思：变量占用内存的事件可能会过长（毕竟延长了局部变量的生命周期嘛~ 申请的内存空间没有被正确释放，导致后续程序里这块内存被永远占用（不可达））——

  > 简单来说就是：闭包会常驻内存，增加内存使用量。

  所以需要及时释放——

  

  【2.1】解决内存泄漏的方法让**内部函数对象**f成为垃圾对象！！

  ```js
   f = null;// 解放空间！
  ```

  【2.2】我们可以利用垃圾回收机制销毁内存中的闭包或者手动销毁，上面提到了手动销毁，而垃圾回收机制有如下方法——

  - 标记清除法
  - 循环计数法

## 3、算法：说一下递归和迭代的区别是什么，各有什么优缺点？

> 这里感觉非常新奇呐！之前没有研究过！

（一）定义：

- **递归**: 递归常被用来描述以自相似方法重复事物的过程，在数学和开发中，指的是在函数定义中使用函数自身的方法；递归实际上不断地深层调用函数，直到函数有返回才会逐层的返回，递归是用栈机制实现的，每深入一层，都要占去一块栈数据区域，因此，递归涉及到运行时的堆栈开销（参数必须压入堆栈保存，直到该层函数调用返回为止），所以有可能导致堆栈溢出的错误；但是递归编程所体现的思想正是人们追求简洁、将问题交给计算机，以及将大问题分解为相同小问题从而解决大问题的动机。递归，还有个尾调用优化，尾调用优化就是如果本次调用的返回值，是子调用的返回值的话，本次调用就可以直接出栈了，不需要进行嵌套。就可以实现栈深为1的递归调用。递归从字面可以其理解为重复“递推”和“回归”的过程（递推：层层推进，分解问题；回归：层层回归，返回较大问题的解）

  > 简单来说：程序调用自身称为递归

  > - 这里可以看我之前写的一篇剖析递归过程的文章[掌握递归调用栈思想 由浅入深研究递归🎉 - 掘金 (juejin.cn)](https://juejin.cn/post/7016324095843237901#heading-0)，带上图片和例子一起理解

- **迭代**: 是重复反馈过程的活动，其目的通常是为了接近并到达所需的目标或结果。每一次对过程的重复被称为一次“迭代”，而每一次迭代得到的结果会被用来作为下一次迭代的初始值。迭代是顺序的，不涉及调用栈操作，前面的代码不会被后面代码影响，递归是涉及到调用栈的，遵循先入栈后结束后入栈先结束原则，前面的函数调用会阻塞，要在后面的调用返回值后才能继续执行，所以迭代的好处就是栈深小，但是代码逻辑不够清晰，递归则是嵌套调用多，栈深比较大，容易爆栈，但代码结构会比较简洁，速度的话还是迭代快。迭代大部分时候需要人为的对问题进行剖析，分析问题的规律所在，将问题转变为一次次的迭代来逼近答案。迭代不像递归那样对堆栈有一定的要求，另外一旦问题剖析完毕，就可以很容易的通过循环加以实现。迭代的效率高，但却不太容易理解，当遇到数据结构的设计时，比如图表、二叉树、网格等问题时，使用就比较困难，而是用递归就能省掉人工思考解法的过程，只需要不断的将问题分解直到返回就可以了。

  > 简单来说：利用变量的原值推出新值称为迭代。

（二）异同点：

> 了解一下递归和迭代的时间复杂度！感觉蛮加分的~

- 相同点：递归和迭代都是循环的一种。

- 不同点：
  - （1）**程序结构不同**：递归是重复调用函数自身实现循环。迭代是函数内某段代码实现循环。 其中，迭代与普通循环的区别是：迭代时，循环代码中参与运算的变量同时是保存结果的变量，当前保存的结果作为下一次循环计算的初始值。	
  - （2）**算法结束方式不同**（递归的一大要素——结束条件）：递归循环中，遇到满足终止条件的情况时逐层返回来结束。迭代则使用计数器结束循环。 当然很多情况都是多种循环混合采用，这要根据具体需求。
  - （3）**效率不同**：在**循环的次数较大的时候，迭代的效率明显高于递归**
  - （4）**运行过程不同**，如果是循环迭代的话，这个整个就在主函数的或者在调用函数的栈空间里面，如果是递归的话，它会不断的申请函数调用的栈空间，在计算的过程中，计算一个结果，退一层栈，递归过程，在调用的时候有可能会出现栈的溢出。
  - （5）理论上递归和迭代时间复杂度方面是一样的，但**实际应用中（函数调用和函数调用堆栈的开销）递归比迭代效率要低**。

（三）优缺点

- 递归的
  - 优点: 大问题转化为小问题，可以减少代码量，同时代码精简，可读性好。
  - 缺点: 递归调用**浪费了空间**（递归调用栈），而且递归太深容易造成堆栈的溢出。

- 迭代的
  - 优点: 就是代码运行效率好，因为时间只因循环次数增加而增加，而且没有额外的空间开销。
  - 缺点: 就是代码不如递归简洁

## 4、[力扣101.对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

> [相关讨论](https://github.com/FangzhouSu/FE-Harvester-studyEveryday/issues/1#issuecomment-1010753085)

![image-20220112184746023](https://gitee.com/su-fangzhou/blog-image/raw/master/202201121847142.png)

- `DFS深搜递归法`

```js
var isSymmetric = function(root) {
    // 先dfs深搜到最下面，验证局部对称性
    function dfs(left, right) {
        // 遍历到叶节点，返回true
        if(left === null && right === null) {
            return true
        }
        // 遍历到只有一个子节点的节点，返回false
        if(left === null || right === null) {
            return false
        }
        // 遍历到两个不相等的节点，返回false
        if(left.val !== right.val) {
            return false
        }
        // 递归比较左节点的左孩子和右节点的右孩子&&左节点的右孩子和右节点的左孩子
        // 这一步 将递归函数dfs不断加入递归调用栈，进行局部对称性的验证
        return dfs(left.left, right.right) && dfs(left.right, right.left)
    }
    return dfs(root.left, root.right)
};
```

- `队列+迭代法`

```js
var isSymmetric = function(root) {
  //迭代方法判断是否是对称二叉树
  //首先判断root是否为空
  if(root===null){
      return true;
  }
  let queue=[];
  queue.push(root.left);
  queue.push(root.right);
  while(queue.length){
      let leftNode=queue.shift();//左节点
      let rightNode=queue.shift();//右节点
      if(leftNode===null&&rightNode===null){
          continue;
      }
      if(leftNode===null||rightNode===null||leftNode.val!==rightNode.val){
          return false;
      }
      queue.push(leftNode.left);//左节点左孩子入队
      queue.push(rightNode.right);//右节点右孩子入队
      queue.push(leftNode.right);//左节点右孩子入队
      queue.push(rightNode.left);//右节点左孩子入队
  }
  return true;
};
```

- `栈+迭代`

```js
var isSymmetric = function(root) {
  //迭代方法判断是否是对称二叉树
  //首先判断root是否为空
  if(root===null){
      return true;
  }
  let stack=[];
  stack.push(root.left);
  stack.push(root.right);
  while(stack.length){
      let rightNode=stack.pop();//左节点
      let leftNode=stack.pop();//右节点
      if(leftNode===null&&rightNode===null){
          continue;
      }
      if(leftNode===null||rightNode===null||leftNode.val!==rightNode.val){
          return false;
      }
      stack.push(leftNode.left);//左节点左孩子入队
      stack.push(rightNode.right);//右节点右孩子入队
      stack.push(leftNode.right);//左节点右孩子入队
      stack.push(rightNode.left);//右节点左孩子入队
  }
  return true;
};
```

