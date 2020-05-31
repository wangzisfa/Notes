# 【从零开始的JavaScript】之js基础知识

## JavaScript的使用

- 内部脚本：将脚本置于 <body> 元素底部 可改善显示速度！
- 外部脚本：外部脚本不能包含 <script> 标签

外部脚本 的 **优势** ：已缓存的 js 文件可以加速页面加载



### js 的显示方案

输出显示至：

- 警告框
- HTML输出
- HTML元素
- 浏览器控制台



#### 根据HTML元素输出

```HTML
<h1 id="words">
    hello world
</h1>
<script>
document.getElementById("words").innerHTML = "hell world";
</script>
```