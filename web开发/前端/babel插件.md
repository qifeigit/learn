Babel 插件实践

Babel介绍

babel是一个通用的多功能 JavaScript 编译和转译器，并且在依赖不同的拓展插件下可用于不同形式的静态分析，比如语法检查、编译、代码高亮、代码转换、优化、压缩等。

Compiler Transpiler Interpreter

**Compiler** - compiles code to a lower level code.

Example:

- "Developer code" -> "Machine code"
- PHP -> C
- Java -> bytecode

**Transpiler** - compiles code to same level of code/abstraction.

Example:

- "Developer code" -> "Another developer code or version"
- JavaScript ES2015+ -> JavaScript ES5

**Interpreter** - interprets code, not really in the same class/league/context with the two above.

Example: php.exe

- "Your PHP code/scripts inside index.php" -> "Results to html or just like pure index.html"

Babel 的处理步骤

Babel 的三个主要处理步骤分别是： **解析（parse）**，**转换（transform）**，**生成（generate）**。

解析

**解析**步骤接收代码并输出 AST。包含词法分析，语法分析。

```
24 * 60 * 60
```

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=feab053258c5365bc8df81e79ae7786e_8f118824ce50c961_boxk4RFfqGG2VXPaXKjXY2KLooN_wygiPqGJvbGyT26xjj14eXJRYUAyNShi)

转换

[转换](https://en.wikipedia.org/wiki/Program_transformation)步骤接收 AST 并对其进行遍历，在此过程中对节点进行添加、更新及移除等操作

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=24ee8902e9a8c2d5be827a4775b66f32_8f118824ce50c961_boxk49K5sv4f4swHrfZ3VTydMtd_5jnQyVDDLjZYttDIIl9Lxiy2jXxSAVJl)

生成

[代码生成](https://en.wikipedia.org/wiki/Code_generation_(compiler))步骤把最终（经过一系列转换之后）的 AST 转换成字符串形式的代码

```
86400
```

遍历

想要转换 AST 你需要进行递归的[树形遍历](https://en.wikipedia.org/wiki/Tree_traversal)。深度优先

Visitors（访问者）

发对于这个遍历过程，babel 通过实例化 visitor 对象完成，既其实我们生成出来的 AST 结构都拥有一个 accept 方法用来接收 visitor 访问者对象的访问，而访问者其中也定义了 visit 方法(即开发者定义的函数方法)使其能够对树状结构不同节点做出不同的处理，借此做到在对象结构的一次访问过程中，我们能够遍历整个对象结构。

**Paths**

Visitors 在遍历到每个节点的时候，都会给我们传入 path 参数，包含了节点的信息以及节点和所在的位置，供我们对特定节点进行修改，之所以称之为 path 是其表示的是两个节点之间连接的对象，而非指当前的节点对象

*|*![img](https://internal-api-space.f.mioffice.cn/space/api/box/stream/download/asynccode/?code=8e0147cdc78ac7e420277f53739ef780_8f118824ce50c961_boxk41Gzm2g2737seBhgE09R3xg_POI4LVFiYcpAcvuJiLYQZPxvibPpYhTc)

实战

Babel的插件模块需要你暴露一个function，function内返回visitor

```
module.export = function(babel){
 return {
  visitor:{
    NumberLiteral(node, parent) {},
    CallExpression(node, parent) {},
  }
 }}
表达式( 表达式(24 * 60) *  60))
```

参考资料

https://astexplorer.net/ ast分析工具

https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md babel 文档

https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/the-super-tiny-compiler.js tiny编译器

https://algorithm-visualizer.org/brute-force/binary-tree-traversal 可视化算法

完整代码

```javascript
var babel = require('babel-core');
var t = require('babel-types');
const visitor = {
 BinaryExpression(path) {
  console.log(path.type);
  const node = path.node;
  let result;
  // 判断表达式两边，是否都是数字
  if (t.isNumericLiteral(node.left) && t.isNumericLiteral(node.right)) {
   
   // 根据不同的操作符作运算
   switch (node.operator) {
    case "+":
     result = node.left.value + node.right.value;
     break
    case "-":
     result = node.left.value - node.right.value;
     break;
    case "*":
     result =  node.left.value * node.right.value;
     break;
    case "/":
     result =  node.left.value / node.right.value;
     break;
    case "**":
     let i = node.right.value;
     while (--i) {
      result = result || node.left.value;
      result =  result * node.left.value;
     }
     break;
    default:
   }
  }
  // // 如果上面的运算有结果的话
  // if (result !== undefined) {
  //  // 把表达式节点替换成number字面量
  //  path.replaceWith(t.numericLiteral(result));
  // }
  // 如果上面的运算有结果的话
  if (result !== undefined) {
  // 把表达式节点替换成number字面量
  path.replaceWith(t.numericLiteral(result));
  let parentPath = path.parentPath;
  // 向上遍历父级节点
  // parentPath && visitor.BinaryExpression.call(this, parentPath);
  }
 }
};
const result = babel.transform("const result = 24 * 2 * 2 * 3",{
 plugins:[
  {visitor}
 ]
});
console.log(result.code); 
```

