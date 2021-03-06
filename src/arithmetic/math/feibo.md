## 斐波那契数列

#### 1. 定义  
公式：a<sub>n</sub> = a<sub>n-1</sub>+a<sub>n-2</sub>  
例子：[0, 1, 1, 2, 3, 5, 8, 13, 21, 34...]

#### 2. 代码实现
```js
// 非递归实现
function fib(max) {
    var t,
        a = 0,
        b = 1,
        arr = [0, 1];
    while (arr.length < max) {
        [a, b] = [b, a + b];
        arr.push(b);
    }
    return arr;
}
//递归实现：缺点：fn(45)之后就崩了，因为递归太深了。
function fn(n){
    if(n===1)return 0;
    if(n===2)return 1;
    return fn(n-1)+fn(n-2)
}
```

#### 3. 优化  
1）空间换时间。给出arr=[0, 1, 1, 2, 3, 5, 8, 13, 21, 34...]，直接arr[i]即可。  
2）具有缓存功能的斐波那契数列
```js
var map = {1:1,2:1};
function fn(n){
    if(!map[n])map[n] = fn(n-1)+fn(n-2)
    return map[n];
}
console.log(fn(40))//102334155
console.log(fn(50))//12586269025
console.log(fn(60))//1548008755920
```
3）使用尾递归优化递归的实现方式
```js
function fns(n,r1=0,r2=1) {
  if(n<=1)return r1
  return fns(n-1,r2,r2+r1)
}
```

#### 4. 应用  
1）一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）？  
思路：比较倾向于找规律的解法，f(1) = 1, f(2) = 2, f(3) = 3, f(4) = 5，  可以总结出f(n) = f(n-1) + f(n-2)的规律，但是为什么会出现这样的规律呢？假设现在6个台阶，我们可以从第5跳一步到6，这样的话有多少种方案跳到5就有多少种方案跳到6，另外我们也可以从4跳两步跳到6，跳到4有多少种方案的话，就有多少种方案跳到6，其他的不能从3跳到6什么的啦，所以最后就是f(6) = f(5) + f(4)；
```js
function fn(n){
    var a=1,b=2;
    while(--n !== 0){
        [a,b] = [b,a+b];
    }
    return a;
}
```