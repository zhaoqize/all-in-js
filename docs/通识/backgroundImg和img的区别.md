## 一、backgroundImg和img的区别

#### 1、本身的区别
- backgroundImg: 是修饰性内容，属于CSS模块
- img：属于页面元素必备内容，属于DOM模块

### 2、加载时机区别
- backgroundImg：会等待页面加载完成再去加载图片，串形处理
- img: 会在解析dom的过程中去加载图片，并行处理

## 二、参考&拓展
- [img标签和background-image的区别和具体使用时机](http://www.cnblogs.com/Jerry-MrNi/p/6536303.html)