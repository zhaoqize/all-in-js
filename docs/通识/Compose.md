## 一、Compose （组合）

组合：就是将两个函数组合成一个新函数。

代码表示：
```
var compose = function(f,g) {
  return function(x) {
    return f(g(x));
  };
};
```

例子：
```
var toUpperCase = function(x) { return x.toUpperCase(); };
var exclaim = function(x) { return x + '!'; };
var shout = compose(exclaim, toUpperCase);

shout("send in the clowns");
//=> "SEND IN THE CLOWNS!"
```

## 二、参考&拓展
- [compose](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/ch5.html#%E5%87%BD%E6%95%B0%E9%A5%B2%E5%85%BB)