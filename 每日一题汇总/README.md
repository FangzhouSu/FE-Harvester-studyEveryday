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



# 22/1/13每日一题

> 1.箭头函数与普通函数的区别?
>
> 2.this指向哪⾥？
>
> 3.扩展运算符的作用及使用场景?
>
> > 仓管来加道经典题 大家来瞅一眼呗hh 昨天做了树 今天做个超级经典数组题吧！
>
> 4.[217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

## 1.箭头函数与普通函数的区别?

> 1.箭头函数的参数只有一个时，可以省略小括号（但是！这里最好是[带上括号](https://github.com/lin-123/javascript#arrows--paren-wrap)哦！），函数里面的执行语句只有一条时，可以省略花括号（但是！如果回调函数没有return 则[最好加上大括号](https://github.com/lin-123/javascript#arrows--implicit-return) ——减少副作用）
> 2.箭头函数本身没有this，它会**继承作用域链上一层的this**
> 3.箭头函数不能使用call, bind, apply来改变this指向

#### 1：写法不一样

```js
function foo() {
    console.log('1')
}
let foo = ()=> {
    console.log('1')
}
```

#### 2：普通函数存在变量提升的现象 箭头函数只会被提升变量

```js
//普通函数
foo()
function foo() {
    console.log('1')
}

//箭头函数
foo() //报错 foo is not a function
let foo = ()=> {
    console.log('1')
}
```

#### 3：箭头函数不能作为构造函数使用

```js
let Person = (name) => {
    this.name = name
}
let xiao_ming = new Person('小明')
console.log(xiao_ming.name) //undefined
```

#### 4：两者this的指向不同

普通函数的this指向的是谁调用该函数就指向谁

箭头函数的this指向的是在你书写代码时候的上下文环境对象的this，如果没有上下文环境对象，那么就指向最外层对象window。

#### 5：箭头函数的arguments指向它的父级函数所在作用域的arguments

```js
function foo() {
  console.log(arguments)
  let foo1 = () => {
    console.log(arguments)
  }
  foo1()
}
foo('test')

//[Arguments] { '0': 'test' }
//[Arguments] { '0': 'test' }
```

#### 6：箭头函数没有new.target

先说明下new.target是干嘛的，这家伙是用来检测函数是否被当做构造函数使用，他会返回一个指向构造函数的引用。

因为箭头函数不能当做构造函数使用，自然是没有new.target的。

## 2.this指向哪里？

> 其实this指向的问题情况并不多，但是它在不同的执行条件下可能会绑定（指向）不同的对象，如果想要再深入了解，可以看一下coderwhy的[这篇文章](https://mp.weixin.qq.com/s/hYm0JgBI25grNG_2sCRlTA)

- 普通函数中：this->window
- 定时器中：this->window
- 构造函数中：this->当前实例化的对象
- 事件处理函数中：this->事件触发对象
- 在 js 中一般理解就是**谁调用这个 this 就指向谁**

## 3.扩展运算符的作用及使用场景

#### 0.将一个数组转为用逗号分隔的参数序列。

> 这里其实是以下几种方法的本质啦~

```js
console.log(...[1, 2, 3]) // 1 2 3

console.log(1, ...[2, 3, 4], 5) //1 2 3 4 5
```

#### 1.普通函数中使用，用作参数

```js
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

var numbers = [1, 2];
add(...numbers) // 3
```

#### 2.替代 apply 方法 方便地将数组转变为可以传入函数的参数

> 本质也跟0是一样的~

```js
// ES5 的写法
Math.max.apply(null, [14, 3, 77])

// ES6 的写法
Math.max(...[14, 3, 77])

// 等同于
Math.max(14, 3, 77);
```

#### 3.合并数组

```js
var arr1 = ['a', 'b'];
var arr2 = ['c'];
var arr3 = ['d', 'e'];

// ES5的合并数组
arr1.concat(arr2, arr3)  // [ 'a', 'b', 'c', 'd', 'e' ]

// ES6的合并数组
[...arr1, ...arr2, ...arr3]  // [ 'a', 'b', 'c', 'd', 'e' ]
```

#### 4.与解构赋值结合

```js
const [first, ...rest] = [1, 2, 3, 4, 5];
first // 1
rest  // [2, 3, 4, 5]

const [first, ...rest] = [];
first // undefined
rest  // []

const [first, ...rest] = ["foo"];
first  // "foo"
rest   // []
```

如果将扩展运算符用于数组赋值，只能放在参数的最后一位，否则会报错。

> 这个点之前还真没有注意~

```js
const [...butLast, last] = [1, 2, 3, 4, 5];  // 报错

const [first, ...middle, last] = [1, 2, 3, 4, 5];  // 报错
```

#### 5.将字符串转为数组

```js
var str = 'hello';

// ES5  
var arr1 = str.split('');  // [ "h", "e", "l", "l", "o" ] 

// ES6  
var arr2 = [...str];  // [ "h", "e", "l", "l", "o" ] 
```

#### 6.实现了 Iterator 接口的对象

任何Iterator接口的对象，都可以用扩展运算符转为真正的数组。

```js
var domList = document.querySelectorAll('span');
var array = [...domList];
```

#### 7.数组/对象的浅拷贝

```js
const arr = [1, 2, 3];
const copy = [...arr];

const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 };
```

## 4、[217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

经典的数组查重问题！

- 【1】利用判重API `indexOf`构建去重辅助数组

```js
var containsDuplicate = function(nums) {
    let newArr = []
    for(let i = 0; i < nums.length; i++) {
        if(newArr.indexOf(nums[i]) === -1) {
            newArr.push(nums[i])
        }
    }
    return newArr.length !== nums.length
};
```

执行用时较高！想必是`indexOf`方法的锅咯~

- 【2】利用数据结构Set 构造只有单一元素的Set对象,判断Set对象与原数组长度是否相同

```js
var containsDuplicate = function(nums) {
    let newArr = new Set(nums)
    return newArr.size !== nums.length
};
```

- 同理 使用哈希表记录出现的次数也可以~

这里用Set其实更好哈~主要上面刚用过 换个口儿😄

```js
var containsDuplicate = function(nums) {
    let map = new Map()
    for(let i = 0; i < nums.length; i++) {
        if(map.has(nums[i])) {
            return true
        }
        else{
            map.set(nums[i], 1)
        }
    }
    return false
};
```

时间复杂度O(N)

空间复杂度O(N)

- 【3】排序后冒泡比较

这里可以拓展炫技手写个排序出来？😏

```js
var containsDuplicate = function(nums) {
    nums.sort((a, b) => a - b)
    for(let i = 0; i < nums.length - 1; i++) {
        if(nums[i] === nums[i + 1]) {
            return true
        }
    }
    return false
};
```

时间复杂度O(N*log~N~)

空间复杂度O(log~N~) 在这里应当考虑排序时递归调用栈的深度。

>  V8 引擎 sort 函数只给出了两种排序 InsertionSort 和 QuickSort，
>
>  - 数量小于10的数组使用 `InsertionSort`-插入排序
>  - 比10大的数组则使用 `QuickSort`-快速排序
>
>  详情见[V8 引擎array源码](https://github.com/v8/v8/blob/ad82a40509c5b5b4680d4299c8f08d6c6d31af3c/src/js/array.js) 710行开始 快排在760行处



- 【4】说干就干！来手写个快排！参考之前写过的一篇[Java题解](https://blog.csdn.net/qq_45704942/article/details/116448702?spm=1001.2014.3001.5502)（写得贼详细 每一步都拆分开来说了！），这篇文章是参考的leetcode主站的一篇[优秀图解 by 袁厨](https://leetcode-cn.com/problems/sort-an-array/solution/dong-hua-mo-ni-yi-ge-kuai-su-pai-xu-wo-x-7n7g/)~（好家伙连环参考）

快排分以下几步

1.选出基准值

2.使用[填坑法](https://leetcode-cn.com/problems/sort-an-array/solution/dong-hua-mo-ni-yi-ge-kuai-su-pai-xu-wo-x-7n7g/)，写一个partition函数将数组分为小于基准值和大于基准值两部分

3.递归完成快排！

下面代码里这个注释很清楚了吧！

另外还写了个[题解](https://leetcode-cn.com/problems/sort-an-array/solution/javascriptjava-chao-xiang-xi-ti-jie-tian-dsvc/) 搭配图看着更舒服哈~

```js
var sortArray = function(nums) {
    quicksort(nums, 0, nums.length - 1)// 调用快排方法
    return nums
};
var quicksort = function(nums, low, high) {
    if(low < high) {
        let index = partition(nums, low, high)// 得到用来将数组分成两部分（左面全小于index 右面全大于index）的索引
        quicksort(nums, low, index - 1)// 以第一轮得出的index为基准划分出左半区和右半区 对数组的左半区进行递归 将其全部变为有序
        quicksort(nums, index + 1, high)// 同理左半区
    }
}
var partition = function(arr, low, high) {
    let pivot = arr[low]// 选定第一个元素为基准值 把它拿出来 即为“挖坑”
    while(low < high) {
        // 【1】 挖了坑就需要填坑~从high指针开始向左找 
        while(low < high && arr[high] >= pivot) {
            high--
        }
        arr[low] = arr[high]// 一旦找到比坑对应值pivot小的 就扔到low那侧的坑里
        // 【2】 同【1】从low指针开始向右找填坑值
        while(low < high && arr[low] < pivot) {
            low++
        }
        arr[high] = arr[low]// 一旦找到比坑对应值pivot大的 就扔到high那侧的坑里
        //（刚刚这侧有一个值去填low那侧的坑了 所以出现了一个坑位~）
    }
    // 经过上面【1】【2】的不断迭代 low===high 此时这个位置即为基准位置
    arr[low] = pivot
    return low// 分区成功！返回定海神针~（此时low=high哦~）
}
```

> 再拓展补充下~
>
> - 不稳定的四种排序方法 **快选希堆** 
>
> - 最快的排序方法是**归并排序** 还有一个不常见的堆排序！ 时间复杂度为 n×log~n~
>
>   - 快速排序的平均时间复杂度是n×log~n~
>
>   ![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f79a76fa5224409bdcea8ed5cef1470~tplv-k3u1fbpfcp-zoom-1.awebp?)
>
> - 归并排序和快速排序的区别：
>
>   ![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/431ac187d7ac4331abc3702407c3ab16~tplv-k3u1fbpfcp-zoom-1.awebp?)
>
>   - 归并是先拆开 从底下往上面排 
>   - 快排是每次都打乱一下 从上往下排

# 22/1/14每日一题

> 1.讲一下强缓存和协商缓存的区别
> 2.如何解决跨越问题
> 3.对事件委托的理解以及其使用场景
> 4 算法，最大数

## 1.讲一下强缓存和协商缓存的区别

> 强缓存策略和协商缓存策略
>
> > 字节二面原题orz 当时听都没听说过 
> >
> > ”啊？强缓存 对应的是弱缓存么？😫“  ”对应的是协商缓存😑😑“
>
> - 在缓存命中时**都会直接使用本地的缓存副本**；
>
> - 它们缓存不命中时，都会**向服务器发送请求来获取资源**。在实际的缓存机制中，强缓存策略和协商缓存策略是一起**合作使用**的。
>   - **浏览器**首先会根据请求的信息判断**强缓存**是否命中，【1】如果命中则直接使用本地资源的副本。如果不命中则【2】根据头信息向服务器发起请求，使用协商缓存——
>   - 【3】如果**协商缓存**命中的话（资源没有过期，服务器响应报文状态码为304 临时重定向），则**服务器**不返回资源，浏览器直接使用本地资源的副本，如果协商缓存不命中，则服务器返回最新的资源给浏览器。

#### 缓存技术实现

> 对于一些具有重复性的HTTP请求 比如**每次请求得到的数据都是一样的** 我们就可以把这对**请求-响应**的数据都缓存在本地 那么下次就直接读取本地的数据 不必再通过网络获取服务器的响应了~

这样的话HTTP/1.1的性能肯定可以获得肉眼可见的提升！

总结一下上面所说的 避免发送HTTP请求的方法 就是通过==缓存技术==来实现 HTTP设计者早在之前就考虑到了这点 因此**HTTP协议的头部有不少是针对缓存的字段**



#### 缓存技术实现细节

再来刨根问底一下 缓存是如何做到的呢？

> 【1】客户端会把**第一次请求以及相应的数据保存在本地磁盘上**
>
> 其中将请求的URL作为key 而响应作为value 两者形成映射关系 **URL->响应**
>
> 这样 当后续发起相同的请求时 就可以先在本地磁盘上通过key查到对应的value 也就是响应 （前提：资源没有过期）![image-20210810095837315](https://gitee.com/su-fangzhou/blog-image/raw/master/202201150051848.png)
>
> ![image-20210810095923121](https://gitee.com/su-fangzhou/blog-image/raw/master/202201150051236.png)



#### 更新缓存的资源

看到这里 新的问题又会出现了——

万一**缓存的响应不是最新的**，而客户端并不知情 那么该怎么办呢？

这个问题HTTP的设计者也早已考虑到了~

> 服务器在发送HTTP响应时 会**估算一个过期的时间** 并把这个信息放到响应头部中——
>
> 这样客户端在**查看响应头部的信息时，【2】一旦发现缓存的响应是过期的，则就会重新发送网络请求**。（强缓存命中则直接使用本地资源的副本。如果不命中则根据头信息向服务器发起请求，使用协商缓存，也就是接下来的【3】）

HTTP关于缓存说明的头部字段很多~这部分内容之后再仔细研究下 暂时不再拓展了



#### 更新缓存资源细节

最后再来思考一个问题——

> 如果客户端从第⼀次请求得到的响应头部中发现该响应过期了，客户端重新发送请求，假设服务器上的资源并没有 变更，还是⽼样⼦，那么你觉得还要在服务器的响应带上这个资源吗？ 
>
> 很显然不带的话，可以提⾼ HTTP 协议的性能，那具体如何做到呢？

是啊 如果在重新发送请求的时候发现资源并没有变更 那么服务器在响应的时候应该返回什么资源呢？

> 【3】这个就需要我们在客户端重新发送请求时 **在请求的 `Etag` 头部带上第一次请求的响应头部中的摘要**，这个<u>摘要是唯一标识响应的资源</u>，当服务器收到请求后 会将本地资源的摘要（也就是最新的摘要） 与 请求中的摘要（缓存中的摘要）做个比较——
>
> - 如果不同 说明客户端的缓存（URL->响应）已经没有价值 服务器将在响应中带上最新的资源。
>
> ![image-20210810101411121](https://gitee.com/su-fangzhou/blog-image/raw/master/202201150112923.png)
>
> - 如果相同 说明客户端的缓存还是可以继续使用的 那么服务器**仅返回不含有包体的 `304 Not Modified` 响应** 来告诉客户端“缓存的资源仍然有效哦！” 这样可以减少响应资源在网络中传输的延时！
>   - ==协商缓存==
>
> ![image-20210810101704953](https://gitee.com/su-fangzhou/blog-image/raw/master/202201150112612.png)



通过本个问题 - “如何避免发送HTTP请求” 对4个小点的研究

我们发现每一个点都包含了“缓存” 

可以看出来 缓存真的是性能优化的一把万能钥匙！

小到 CPU Cache、Page Cache、Redis Cache

大到HTTP协议的缓存~

## 2.如何解决跨越问题

1.JSONP 使用script标签向后台请求数据，只适用于get请求
2.CORS是让服务器端设置Access-Control-Allow-Origin（头部字段），这样浏览器就不会报跨域错误
3.反向代理，搭建一个自己的服务器，让自己的服务器请求数据，拿到数据之后再返回给我自己

## 3.对事件委托的理解以及其使用场景

事件委托的本质是利用了**浏览器事件冒泡**的机制.

因为**事件在冒泡过程中会上传到父节点**,父节点可以通过事件对象获取到目标节点,因此可以把子节点的监听函数定义在父节点上,由父节点的监听函数统一处理多个子元素的事件,这种方式称为事件委托

事件委托的使用场景 :

1.当存在多个元素可以共用同一个监听器 

2.用事件委托实现动态监控

## 4 算法，最大数

- `巧妙排序`

```js
var largestNumber = function(nums) {
    let sorted = nums.sort((a, b) => {
        if (`${a}${b}` > `${b}${a}`) {
            return -1
        }
        else {
            return 1
        }
    })
    // 存在[0,0] [0,0,0]这种特殊情况 会出现00这种奇怪的答案，所以要删去多余的0
    for (let i = 0; i < sorted.length - 1; i++) {
        if (sorted[i] === 0) {
            sorted.splice(i, 1)
            i--// 防止删除数组中某个元素之后造成的数组塌陷
        }
        else {
            break
        }
    }
    return sorted.join("")
};
```

> 知识点：V8中sort函数的实现机制
>
> `sort()` 方法用[原地算法](https://links.jianshu.com/go?to=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FIn-place_algorithm)对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的
>
> — MDN

> 关于 `Array.prototype.sort()`  ，ES 规范并没有指定具体的算法，在 V8 引擎中，  **7.0 版本之前** ，数组长度小于10时， `Array.prototype.sort()` 使用的是插入排序，否则用快速排序。
>
> 在 V8 引擎 **7.0 版本之后** 就舍弃了快速排序，因为它不是稳定的排序算法，在最坏情况下，时间复杂度会降级到 O(n2)。
>
> 于是采用了一种混合排序的算法：**TimSort** 。
>
> 这种功能算法最初用于Python语言中，严格地说它不属于以上10种排序算法中的任何一种，属于一种混合排序算法：
>
> 在数据量小的子数组中使用**插入排序**，然后再使用**归并排序**将有序的子数组进行合并排序，时间复杂度为 `O(nlogn)` 。
>
> 
>
> 作者：an_371e
> 链接：https://www.jianshu.com/p/a557e9006186
> 来源：简书
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

# 22/1/18每日一题

> 1. cookie sessionstorage localstorage 的区别
> 2. 浏览器的渲染过程
> 3. 渐进增强和优雅降级
> 4. 手写斐波那契数列

## 1.cookie & sessionstorage & localstorage 的区别

- 共同点：都是保存在浏览器端，并且是同源的,都是**字符串类型**的键值对
- cookie数据始终在同源的http请求中携带，每次http请求都会携带cookie，cookie的数据大小不能超过4KB 
  - sessionstorage和localstorage可以达到5MB
- sessionstorage:仅在**浏览器窗口关闭前有效**，不能长久保存
- localstorage：数据始终有效，窗口或浏览器关闭也一直存在

## 2.浏览器的渲染过程

【1】解析 HTML 构建DOM树

【2】解析CSS 构建CSSOM树

【3】利用上面两个树构建渲染树（渲染树的节点即为“渲染对象”）

【4】渲染对象被创建并添加到树中，它们并没有位置和大小，所以当浏览器生成渲染树以后，就会根据渲染树来进行布局（也可以被称作“**回流**”）这一阶段浏览器要做的事情是要弄清楚各个节点在页面中的确切位置和大小。通常这一行为也被称为“**自动重排**”。

【5】上述几步过后，布局结束；最后进行绘制，遍历渲染树并调用渲染对象的 paint 方法将它们的内容显示在屏幕上，绘制使用 UI 基础组件。

记住这张图：

[![image](https://camo.githubusercontent.com/ab5629cbfbeeaa676befdf1033d0481d37d67fc33c6979ff195752915959f6b4/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f79757175652f302f323032302f706e672f313530303630342f313630333739373933393136352d33626635346532382d353436392d343039332d613065312d6530353639636563313330352e706e67)](https://camo.githubusercontent.com/ab5629cbfbeeaa676befdf1033d0481d37d67fc33c6979ff195752915959f6b4/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f79757175652f302f323032302f706e672f313530303630342f313630333739373933393136352d33626635346532382d353436392d343039332d613065312d6530353639636563313330352e706e67)

## 3.渐进增强和优雅降级

- 渐进增强:是针对低版本浏览器构建页面，保证最基本的功能，然后针对高版本浏览器进行效果，交互等改进并追加功能，达到更好的用户体验
- 优雅降级：一开始就构建完整功能，然后**对低版本浏览器进行兼容**适配

## 4.手写斐波那契数列

- `简单的动归解法`

```js
let fib = function(n) {
    let dp = [0, 1]
    for(let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2]
    }
    console.log(dp)
    return dp[n]
};
```

- `超简单的递归`

```js
let fb = function(n) {
    if (n === 0) {
        return 0
    }
    if (n === 1) {
        return 1
    }
    return fb(n - 1) + fb(n - 2)
};
```

- 记忆化搜索提升效率

[斐波那契数列 - cj-ervin的个人空间 - OSCHINA - 中文开源技术交流社区](https://my.oschina.net/u/4074923/blog/4274493)

# 22/1/19每日一题

> ​	1.字面量new出来的对象和Object.create(null)创建出来的对象有什么区别？
> 2. 数据类型检测的方式都有哪些?
> 3. 判断数组检测的方式都有哪些?
> 4. new的具体操作过程

## 1.字面量new出来的对象和Object.create(null)创建出来的对象有什么区别？

- new创建出来的对象会**继承Object的方法和属性**，创建出来的对象的隐式原型（**proto**)会指向Object的显示原型；
- 而Object.create(null)创建出来的对象原型为null，作为**原型链的顶端**，就**没有继承Object的方法和属性**。

## 2.数据类型检测的方式都有哪些?

**（1）typeof**

```javascript
console.log(typeof 2);               // number
console.log(typeof true);            // boolean
console.log(typeof 'str');           // string
console.log(typeof []);              // object    
console.log(typeof function(){});    // function
console.log(typeof {});              // object
console.log(typeof undefined);       // undefined
console.log(typeof null);            // object
```

其中**数组、对象、null**都会被判断为object，其他判断都正确。



**（2）instanceof**

`instanceof`可以正确判断对象的类型，**其内部运行机制是判断在其原型链中能否找到该类型的原型**。

```javascript
console.log(2 instanceof Number);                    // false
console.log(true instanceof Boolean);                // false 
console.log('str' instanceof String);                // false 
 
console.log([] instanceof Array);                    // true
console.log(function(){} instanceof Function);       // true
console.log({} instanceof Object);                   // true
```

可以看到，`instanceof`**只能正确判断引用数据类型**，而**不能判断基本数据类型**。`instanceof` 运算符可以用来测试一个对象在其原型链中是否存在一个构造函数的 `prototype` 属性。



**（3） constructor**

```javascript
console.log((2).constructor === Number); // true
console.log((true).constructor === Boolean); // true
console.log(('str').constructor === String); // true
console.log(([]).constructor === Array); // true
console.log((function() {}).constructor === Function); // true
console.log(({}).constructor === Object); // true
```

`constructor`有两个作用，一是判断数据的类型，二是对象实例通过 `constructor` 对象访问它的构造函数。需要注意，如果创建一个对象来改变它的原型，`constructor`就不能用来判断数据类型了：

```javascript
function Fn(){};
 
Fn.prototype = new Array();
 
var f = new Fn();
 
console.log(f.constructor===Fn);    // false
console.log(f.constructor===Array); // true
```

**（4）Object.prototype.toString.call()**

`Object.prototype.toString.call()` 使用 Object 对象的原型方法 toString 来判断数据类型：

```javascript
var a = Object.prototype.toString;
 
console.log(a.call(2));
console.log(a.call(true));
console.log(a.call('str'));
console.log(a.call([]));
console.log(a.call(function(){}));
console.log(a.call({}));
console.log(a.call(undefined));
console.log(a.call(null));
```

同样是检测对象obj调用toString方法，obj.toString()的结果和Object.prototype.toString.call(obj)的结果不一样，这是为什么？



这是因为toString是Object的原型方法，而Array、function等**类型作为Object的实例，都重写了toString方法**。不同的对象类型调用toString方法时，根据原型链的知识，调用的是对应的重写之后的toString方法（function类型返回内容为函数体的字符串，Array类型返回元素组成的字符串…），而不会去调用Object上原型toString方法（返回对象的具体类型），所以采用obj.toString()不能得到其对象类型，只能将obj转换为字符串类型；因此，在想要得到对象的具体类型时，应该调用Object原型上的toString方法。



## 3 判断数组检测的方式都有哪些?

- 通过`Object.prototype.toString.call()`做判断

```javascript
Object.prototype.toString.call(obj).slice(8,-1) === 'Array';
```

- 通过原型链做判断

```javascript
obj.__proto__ === Array.prototype;
```

- 通过ES6的Array.isArray()做判断

```
Array.isArray(obj);
```

- 通过instanceof做判断

```javascript
obj instanceof Array
```

- 通过Array.prototype.isPrototypeOf

```javascript
Array.prototype.isPrototypeOf(obj)
```



## 4. new的具体操作过程

> 红宝书权威解释
>
> ![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f493f86148bf4a3c888e34b6f6fd79c1~tplv-k3u1fbpfcp-watermark.awebp?)

更细致的内容之前我有总结过一篇，相当于是手写`new Object`吧~[JS小知识 new关键字都做了什么？ - 掘金 (juejin.cn)](https://juejin.cn/post/7012887169878458404)

# 1/20每日一题

> 1、实现一个三角形
> 2、JavaScript为什么要进行变量提升，它导致了什么问题？
> 3、实现节流函数和防抖函数



# 1/21每日一题

> 1.HTTP: 1.0 1.1 2.0 3.0对应的改进点，2.0实现多路复用的底层原理？
>
> 2.Js:  call、apply、bind作用和区别
>
> 3.数据结构: Map 和 Set 的区别

## 1.HTTP: 1.0 1.1 2.0 3.0对应的改进点，2.0实现多路复用的底层原理？

### **HTTP 1.0和 HTTP 1.1** **有以下区别**：

- **连接方面**，http1.0 默认使用非持久连接，而 http1.1 默认使用持久连接。http1.1 通过使用持久连接来使多个 http 请求复用同一个 TCP 连接，以此来避免使用非持久连接时每次需要建立连接的时延。
- **资源请求方面**，在 http1.0 中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，http1.1 则在请求头引入了 range 头域，它允许只请求资源的某个部分，即返回码是 206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
- 3.数据结构: Map 和 Set 的区别**缓存方面**，在 http1.0 中主要使用 header 里的 If-Modified-Since、Expires 来做为缓存判断的标准，http1.1 则引入了更多的缓存控制策略，例如 Etag、If-Unmodified-Since、If-Match、If-None-Match 等更多可供选择的缓存头来控制缓存策略。
- http1.1 中**新增了 host 字段**，用来指定服务器的域名。http1.0 中认为每台服务器都绑定一个唯一的 IP 地址，因此，请求消息中的 URL 并没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个虚拟主机，并且它们共享一个IP地址。因此有了 host 字段，这样就可以将请求发往到同一台服务器上的不同网站。
- http1.1 相对于 http1.0 还新增了很多**请求方法**，如 PUT、HEAD、OPTIONS 等。

### HTTP 1.1 和 HTTP 2.0 的区别

- **二进制协议**：HTTP/2 是一个二进制协议。在 HTTP/1.1 版中，报文的头信息必须是文本（ASCII 编码），数据体可以是文本，也可以是二进制。HTTP/2 则是一个彻底的二进制协议，头信息和数据体都是二进制，并且统称为"帧"，可以分为头信息帧和数据帧。 帧的概念是它实现多路复用的基础。
- **多路复用：**HTTP/2 实现了多路复用，HTTP/2 仍然复用 TCP 连接，但是在一个连接里，客户端和服务器都可以同时发送多个请求或回应，而且不用按照顺序一一发送，这样就避免了"队头堵塞"【1】的问题。
- **数据流：**HTTP/2 使用了数据流的概念，因为 HTTP/2 的数据包是不按顺序发送的，同一个连接里面连续的数据包，可能属于不同的请求。因此，必须要对数据包做标记，指出它属于哪个请求。HTTP/2 将每个请求或回应的所有数据包，称为一个数据流。每个数据流都有一个独一无二的编号。数据包发送时，都必须标记数据流 ID ，用来区分它属于哪个数据流。
- **头信息压缩：**HTTP/2 实现了头信息压缩，由于 HTTP 1.1 协议不带状态，每次请求都必须附上所有信息。所以，请求的很多字段都是重复的，比如 Cookie 和 User Agent ，一模一样的内容，每次请求都必须附带，这会浪费很多带宽，也影响速度。HTTP/2 对这一点做了优化，引入了头信息压缩机制。一方面，头信息使用 gzip 或 compress 压缩后再发送；另一方面，客户端和服务器同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，以后就不发送同样字段了，只发送索引号，这样就能提高速度了。
- **服务器推送：**HTTP/2 允许服务器未经请求，主动向客户端发送资源，这叫做服务器推送。使用服务器推送提前给客户端推送必要的资源，这样就可以相对减少一些延迟时间。这里需要注意的是 http2 下服务器主动推送的是静态资源，和 WebSocket 以及使用 SSE 等方式向客户端发送即时数据的推送是不同的。

### HTTP3.0的特点

HTTP/3基于UDP协议实现了类似于TCP的多路复用数据流、传输可靠性等功能，这套功能被称为QUIC协议。

![image](https://cdn.nlark.com/yuque/0/2020/webp/1500604/1604068246276-9b0f553d-3c6e-43a3-8185-8565f9fa1fb4.webp)

1. 流量控制、传输可靠性功能：QUIC在UDP的基础上增加了一层来保证数据传输可靠性，它提供了数据包重传、拥塞控制、以及其他一些TCP中的特性。
2. 集成TLS加密功能：目前QUIC使用TLS1.3，减少了握手所花费的RTT数。
3. 多路复用：同一物理连接上可以有多个独立的逻辑数据流，实现了数据流的单独传输，解决了TCP的队头阻塞问题。

![image](https://cdn.nlark.com/yuque/0/2020/webp/1500604/1604068246276-5d0a5de2-00db-425e-8b21-0cc4bbb54b24.webp)

4. 快速握手：由于基于UDP，可以实现使用0 ~ 1个RTT来建立连接。



## 2.call() 和 apply() bind()

它们的作用一模一样，区别仅在于**传入参数的形式的不同**。

- apply 接受两个参数，第一个参数指定了函数体内 this 对象的指向，第二个参数为一个带下标的集合，这个集合可以为数组，也可以为类数组，apply 方法把这个集合中的元素作为参数传递给被调用的函数。
- call 传入的参数数量不固定，跟 apply 相同的是，第一个参数也是代表函数体内的 this 指向，从第二个参数开始往后，每个参数被依次传入函数。

**（1）call 函数的实现步骤：**

- 判断调用对象是否为函数，即使是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
- 判断传入上下文对象是否存在，如果不存在，则设置为 window 。
- 处理传入的参数，截取第一个参数后的所有参数。
- 将函数作为上下文对象的一个属性。
- 使用上下文对象来调用这个方法，并保存返回结果。
- 删除刚才新增的属性。
- 返回结果。

```js
Function.prototype.myCall = function(context) {
  // 判断调用对象
  if (typeof this !== "function") {
    console.error("type error");
  }
  // 获取参数
  let args = [...arguments].slice(1),
    result = null;
  // 判断 context 是否传入，如果未传入则设置为 window
  context = context || window;
  // 将调用函数设为对象的方法
  context.fn = this;
  // 调用函数
  result = context.fn(...args);
  // 将属性删除
  delete context.fn;
  return result;
};
```

**（2）apply 函数的实现步骤：**

- 判断调用对象是否为函数，即使是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
- 判断传入上下文对象是否存在，如果不存在，则设置为 window 。
- 将函数作为上下文对象的一个属性。
- 判断参数值是否传入
- 使用上下文对象来调用这个方法，并保存返回结果。
- 删除刚才新增的属性
- 返回结果

```js
Function.prototype.myApply = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  let result = null;
  // 判断 context 是否存在，如果未传入则为 window
  context = context || window;
  // 将函数设为对象的方法
  context.fn = this;
  // 调用方法
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  // 将属性删除
  delete context.fn;
  return result;
};
```

**（3）bind 函数的实现步骤：**

- 判断调用对象是否为函数，即使是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。
- 保存当前函数的引用，获取其余传入参数值。
- 创建一个函数返回
- 函数内部使用 apply 来绑定函数调用，需要判断函数作为构造函数的情况，这个时候需要传入当前函数的 this 给 apply 调用，其余情况都传入指定的上下文对象。

```js
Function.prototype.myBind = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  // 获取参数
  var args = [...arguments].slice(1),
    fn = this;
  return function Fn() {
    // 根据调用方式，传入不同绑定值
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments)
    );
  };
};
```



## 3.数据结构: Map 和 Set 的区别

### Map

`Map`对象**保存键值对**。任何值(对象或者原始值) 都可以作为一个键或一个值。构造函数`Map`可以接受一个数组作为参数。

**Map和Object的区别**

- 一个`Object` 的键只能是字符串或者 `Symbols`，但一个`Map` 的键可以是任意值。
- `Map`中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
- `Map`的键值对个数可以从 size 属性获取，而 `Object` 的键值对个数只能手动计算。
- `Object` 都有自己的原型，原型链上的键名有可能和你自己在对象上的设置的键名产生冲突。

**Map对象的属性**

- size：返回Map对象中所包含的键值对个数

**Map对象的方法**

- set(key, val): 向Map中添加新元素
- get(key): 通过键值查找特定的数值并返回
- has(key): 判断Map对象中是否有Key所对应的值，有返回true,否则返回false
- delete(key): 通过键值从Map中移除对应的数据
- clear(): 将这个Map中的所有元素删除

**map与其他数据结构的互相转换**

- `Map`与对象的互换

```js
const obj = {}
const map = new Map([['a', 111], ['b', 222]])
for(let [key,value] of map) {
  obj[key] = value
}
console.log(obj) // {a:111, b: 222}
```

- `JSON`字符串要转换成`Map`可以先利用JSON.parse()转换成数组或者对象，然后再转换即可。

### Set

`Set`对象允许你存储任何类型的值，无论是原始值或者是对象引用。它类似于数组，但是成员的值都是唯一的，**没有重复的值**。

`Set` 本身是一个构造函数，用来生成`Set` 数据结构。`Set`函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化。

**Set中的特殊值**

`Set` 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复
- undefined 与 undefined 是恒等的，所以不重复
- NaN 与 NaN 是不恒等的，但是在 Set 中认为NaN与NaN相等，所有只能存在一个，不重复。

**Set实例对象的属性**

- size：返回Set实例的成员总数。

**Set实例对象的方法**

- `add(value)`：添加某个值，返回 Set 结构本身(可以链式调用)。
- `delete(value)`：删除某个值，删除成功返回`true`，否则返回`false`。
- `has(value)`：返回一个布尔值，表示该值是否为Set的成员。
- `clear()`：清除所有成员，没有返回值。

**遍历方法**

- `keys()`：返回键名的遍历器。
- `values()`：返回键值的遍历器。
- `entries()`：返回键值对的遍历器。
- `forEach()`：使用回调函数遍历每个成员。

由于`Set`结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致。



**Set 对象作用**

- 数组去重(利用扩展运算符)

```js
const mySet = new Set([1, 2, 3, 4, 4])
[...mySet] // [1, 2, 3, 4]
```

 

- 合并两个set对象

```js
let a = new Set([1, 2, 3])
let b = new Set([4, 3, 2])
let union = new Set([...a, ...b]) // {1, 2, 3, 4}
```

 

- 交集

```js
let a = new Set([1, 2, 3])
let b = new Set([4, 3, 2])
let intersect = new Set([...a].filter(x => b.has(x)))  // {2, 3} 利用数组的filter方法
```

- 差集

```js
let a = new Set([1, 2, 3])
let b = new Set([4, 3, 2])
let difference = new Set([...a].filter(x => !b.has(x))) //  {1} 
```

### 二者区别

综上所述，主要有一下几个**区别**：

1.**Map是键值对，Set是值的集合**，当然键和值可以是任何的值；

2.Map可以通过get方法获取值，而set不能因为它只有值；

3.都能通过迭代器进行for...of遍历；

4.**Set的值是唯一的可以做数组去重，Map由于没有格式限制，可以做数据存储**

5.map和set都是stl中的关联容器，map以键值对的形式存储，key=>value组成pair，是一组映射关系。set只有值，可以认为只有一个数据，并且set中元素不可以重复且自动排序。



# 1/22 每日一题

> 1. JavaScript中对象继承的方式有哪些
> 2. 实现脚本异步加载方法的关键字有哪些
> 3. 什么是JS事件循环，事件循环机制是什么
> 4. 力扣第20题有效的括号

## 1. JavaScript中对象继承的方式有哪些？

- 原型式继承

    - ```js
        // 原型式继承
        // Object()可以理解为对传入的对象进行一个浅复制
        let person = {
            name: 'szj',
            friends: ['zy', 'wjr', 'ghk']
        }
        
        let me = Object(person);
        me.friends.push('ssss')
        console.log(me);
        console.log(person)
        
        //{ name: 'szj', friends: [ 'zy', 'wjr', 'ghk', 'ssss' ] }
        //{ name: 'szj', friends: [ 'zy', 'wjr', 'ghk', 'ssss' ] }
        
        ```

- 寄生式继承

    - ```js
        // 寄生继承
        // 像是对原型继承的另一种升级 , 采用了工厂模式的方法 增加了对象的方法
        let jisheng = {
            name : 'sss',
            friends: ['ss' , 'www']
        }
        
        const js = (obj) =>{
              const clone = Object(obj);
              clone.sayHi = function (){
                  console.log(clone.name);
              }
              return clone
        }
        
        const m = js(jisheng);
        m.sayHi();
        // sss
        ```

- 组合继承

    - ```js
        // 组合继承
        // 原型链 ＋ 盗用构造函数
        function Super(name){
                this.name = name;
                this.friends = ['szj' , 'zy'];
        }
        Super.prototype.sayName  = function (){
            console.log(this.name);
        }
        
        function Sub(name){
                // 盗用构造函数
                Super.call(this , name);
        }
        // 原型链继承
        Sub.prototype = new Super;
        
        const bob  = new Sub('szj');
        bob.sayName()
        console.log(bob.friends);
        // szj
        // [ 'szj', 'zy' ]
        ```

- 寄生式组合继承

    - ```js
        // 寄生式组合继承
        // 最佳实践!! 相比于组合继承 减少了构造函数调用的次数
        function Superr (name){
            this.name = name;
            this.friends = ['ss' , 'www' , 'ppp'];
        }
        Superr.prototype.say = function (){
            console.log(this.name);
        }
        
        function Subb(name){
            Superr.call(this , name)
        }
        
        function inheritPrototype (sub , superr) {
            const prototype = Object(superr.prototype);
            // 别忘了原型对象的指向
            prototype.constructor = sub;
            sub.prototype = prototype;
        }
        
        inheritPrototype(Subb , Superr);
        const zy = new Subb('zy');
        zy.say()
        console.log(zy.friends);
            // zy
            // [ 'szj', 'zy' ]
        ```

## 2. 实现异步加载方法的关键字有哪些？

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1500604/1603547262709-5029c4e4-42f5-4fd4-bcbb-c0e0e3a40f5a.png)

- defer 
- async
- 总结：
    - 两者都是用来异步加载外部脚本的关键字
    - defer 加载完成后 页面渲染后执行
    - async 加载完成后 立即执行
    - **多个 defer 按顺序依次执行**  ， 多个async执行顺序不定

## 3. 什么是JS的事件循环 ， 事件循环机制是什么？

![image](https://cdn.nlark.com/yuque/0/2021/png/1500604/1615476500217-472563e1-de67-403f-baa7-0fd574d0e618.png?x-oss-process=image%2Fresize%2Cw_1500)

如图： JS是单线程的 ， 在代码执行时，会将代码压入执行栈中保证函数的有序执行 ， 遇到异步任务会将 任务抛给webapi进行处理 ， 处理之后将回调函数推到任务队列（宏任务队列 ， 微任务队列） ， 当执行栈为空时 ， 先执行微任务队列中的函数 ， 如果需要渲染页面 ， 则会渲染页面 ， 最后执行宏任务队列中的函数。

Event Loop 执行顺序如下所示：

- 首先执行同步代码，这属于宏任务
- 当执行完所有同步代码后，执行栈为空，查询是否有异步代码需要执行
- 执行所有微任务
- 当执行完所有微任务后，**如有必要会渲染页面**
- 然后开始下一轮 Event Loop，执行宏任务中的异步代码

宏任务

- 微任务包括： promise 的回调、node 中的 process.nextTick 、对 Dom 变化监听的 MutationObserver。
- 宏任务包括： script 脚本的执行、setTimeout ，setInterval ，setImmediate 一类的定时事件，还有如 I/O 操作、UI 渲染等。

## 4 [leetcode 20 有效的括号 ](https://leetcode-cn.com/problems/valid-parentheses/)
```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    const stack = [];
    for(let i = 0 ; i < s.length ; i++){
        const c = s[i];
        if(c === '{' || c === '[' || c === '('){
            stack.push(c)
        }else{
            const m = stack[stack.length - 1]
            if((m === '{' && c === '}') || (m==='[' && c === ']') || (m === '(' && c ===')')){
                stack.pop();
            }else{
                return false
            }
        }
    }
    return stack.length === 0 ? true : false
};
```

> @[敲代码的小提琴手](https://leetcode-cn.com/u/billsu/)

```js
var isValid = function(s) {
  let map = new Map([
    ['(', ')'],
    ['{', '}'],
    ['[', ']'],
  ]);
  const stack = [];
  for (let i = 0; i < s.length; i++) {
    if (map.has(s[i])) {
      // 找到左括号 入栈
      stack.push(s[i]); 
    } else if (map.get(stack[stack.length - 1]) !== s[i]) {
      // 左右括号不匹配 字符串无效
      return false; 
    } else {
      // 找到匹配得右括号 弹栈
      stack.pop(); 
    }
  }
  return !stack.length;
};
```

# 1/23 每日一题

> 1. let、const、var区别
> 2. 数组去重的方法有哪些？
> 3. vue双向绑定的原理
> 4. 力扣第70题 爬楼梯

## 1. let、const、var区别

- 作用域
    - let 、 const 为块级作用域 
    - var为函数作用域
- 是否可以重复声明
    - let var 可以重复声明
    - const 不可以重复声明
- 变量提升
    - var 具有变量提升
- 暂时性死区
    - let 、const 具有暂时性死区 ， 未声明之后不能使用
- 给全局添加属性
    - var 可以给全局添加属性 let const 不会
- 初始值设置
    - var let 声明时可以不设置初始值
    - const 必须设置初始值
- 指针的指向
    - let 可以修改指针的指向（重新赋值） ， const 不能够修改指针的指向不可以重新赋值，但是引用数据类型的属性可以改变

| **区别**           | **var** | **let** | **const** |
| ------------------ | ------- | ------- | --------- |
| 是否有块级作用域   | ×       | ✔️       | ✔️         |
| 是否存在变量提升   | ✔️       | ×       | ×         |
| 是否添加全局属性   | ✔️       | ×       | ×         |
| 能否重复声明变量   | ✔️       | ×       | ×         |
| 是否存在暂时性死区 | ×       | ✔️       | ✔️         |
| 是否必须设置初始值 | ×       | ×       | ✔️         |
| 能否改变指针指向   | ✔️       | ✔️       | ×         |

## 2. 数组去重的方法有哪些？

##### 1. 数组元素比较型

- 双层`for`循环

    - ```
        // 双层for循环
        // 前一个跟之后所有进行比较 ， 重复了删除掉
        function uniq(arr){
        	for(let i = 0 ; i < arr.length - 1 ; i++){
        		for(let j = i + 1 ; j < arr.length; j++){
        			if(arr[i] === arr[j]){
        				arr.splice(i , 1);
        				// 删除后下表移动到原位置
        				j--;
        			}
        		}
        	}
        	return arr;
        }
        
        ```

- 排序后 相邻位置进行比较

    - ```
        // 排序进行后进行相邻比较
        function sortQ(arr){
        	// 排序后
        	// 没参数 如果没有指明 compareFunction ，那么元素会按照转换为的字符串的诸个字符的Unicode位点进行排序。
        	arr.sort();
        	for(let i = 0 ; i < arr.length - 1 ; i++){
        		if(arr[i] === arr[i + 1]){
        			arr.splice(i , 1);
        			i--;
        		}
        	}
        
        }
        ```

##### 2.查找元素位置型

- `indexOf` 查找元素并返回其第一个索引值

    - ```
        function uniq(arr){
        	const res = [];
        	for(let i = 0 ; i < arr.length ; i++){
        		if(arr.indexOf(arr[i]) === i){
        			res.push(arr[i])
        		}
        	}
        	return res;
        }
        ```

- `findIndex `  返回数组中第一个满足测试函数的元素的索引

    - ```
        function uniq(arr){
        	const res = [];
        	for(let i = 0 ; i < arr.length ; i++){
        		if(arr.findIndex(item => item === arr[i]) === i ){
        			res.push(arr[i]);
        		}
        	}
        	return res;
        }
        ```

##### 3. 查找元素存在型

- `includes` 

    - ```
        // 查找元素存在型
        function uniq(arr){
        	const res = [];
        	for(let i = 0 ; i < arr.length ; i++){
        		if(!res.includes(arr[i])){
        			res.push(arr[i])
        		}
        	}
        	return res;
        }
        ```

##### 4. 利用数据结构类型

- set

    - ```
        // set
        function uniq(arr){
        	return [...new Set(arr)]
        }
        ```

- map

    - ```
        function uniq(arr){
        	const map = new Map();
        	arr.forEach(item =>{
        		map.set(item , true)
        	})
        	// 返回键值 Object.keys（key）
        	return[...map.keys()]
        }
        ```

##### 5. 总结

在简单的测试用例大概 2000 万条数据下，`indexOf` 的方案速度相对最快

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/12/26/16f423b56fc0c430~tplv-t2oaga2asx-watermark.awebp)

## 3. vue双向绑定的原理

- Mvc 模式  到  mvvm模式 的转变 

![img](https://wfx7jb3ja4.feishu.cn/space/api/box/stream/download/asynccode/?code=NWVkNGQyYzg4MzMyMjcxZDViZmY1OGEyN2NhZTY4OTlfZWdGbzdlY1NsVEFDYTNCQW1sWTl3eU8xWHJXS092VlJfVG9rZW46Ym94Y253MG5TenpERXBPNTlXNHlqVzVocXBoXzE2NDI5NDcyMTI6MTY0Mjk1MDgxMl9WNA)



- Mvc 模式 controler 层要大量的控制dom
- Mvvm 模式 是真正做到了数据与视图的分离，  view 和 model 改变时 ， vm层自动进行数据和视图的同步

- vue.js 采用数据劫持结合发布者-订阅者模式的方式 ， 通过Object.defineProperty()来劫持各个属性的setter、getter，在数据监听时发布消息给订阅者 ， 触发响应的监听回调
- 发布 订阅者模式让双向绑定更有效率（一对多）
- 实现一个数据监听器 Observer 
    - 核心是 Object.defineProperty() ， 将Observe的数据对象进行递归遍历 ， 包括子属性的对象加上setter getter方法 ， 赋值时就会调用setter方法，就监听到了数据变化
    - 通知订阅者
- 实现Compile 
    - 解析模板的指令 ， 将模板中的变量替换成数据 ，
    - 初始化页面渲染 ， 
    - 并绑定更新函数 ， 添加监听数据的订阅者 ， 一但数据有变化 ， 更新视图 --绑定更新函数
- 实现watcher （解析 compile 和 observe 的桥梁）
    - 实例化在订阅者添加自己
    - 自己有一个update()方法  --添加订阅者
    - 待属性变动 ， 接受通知，调用自身的update() , 并触发compile中的回调 --》更新视图
- 整合形成一个mvvm

![img](https://wfx7jb3ja4.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWEyMjFkYTYxNTc1MWFjNmE5OWU5ZmI0YjA0ZmUyZDhfa3k5Tzdud1p0ZzQ0cURsZHk1dUo5VVRudXFDd2dRb3hfVG9rZW46Ym94Y240cmRGa1kwYnloNDlWTnA4YzR1dVhmXzE2NDI5NDcyMTI6MTY0Mjk1MDgxMl9WNA)

## 4.[70. 爬楼梯 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/climbing-stairs/)

- 经典dp

```
var climbStairs = function(n) {
    const dp = [];
    dp[0] = 1;
    dp[1] = 1
    for(let i = 2 ; i <= n ; i++){
        dp[i] = dp[i - 1] + dp[i - 2];
    } 
    return dp[n]

};
```



