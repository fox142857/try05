---
title: 01-TypeScript基础
---
# TypeScript
## 一、TypeScript 初体验
### 介绍
> TypeScript 是微软开发的一个开源的编程语言,通过在JavaScript 的基础上添加静态类型定义构建而成. TypeScript 通过 TypeScript编译器 或 Babel 转译为 JavaScript 代码,可运行在任何浏览器,任何操作系统。


![简介](./asset/01/image001.gif)
- 看了上面的介绍, 还是不太明白 TypeScript 是什么, 来看下面的例子,	一段很简单的 js 代码
```js
// 封装函数, 求两数之和
function and(a, b) {
    return a + b
}
```
- 接下来就调用一下试试 `const res = and(10, 20)`
- 这么简单的内容, 谁不会, 这玩意会有什么问题 ?
  + 我们来思考一下, 假设这个函数你在调用的时候
  + 你少传递了一个数字
  + 你传递了一个字符串
  + 会不会出现问题呢 ? 
  + 你可能不禁要问 : 我为什么要少传递一个数字, 为什么要传递字符串呢 ?
  + 可能这个函数略显简单了一些
  + 那么我们在看一个稍微复杂一些的代码
```js
  var times = ''
  function move(ele, target, cb) {
      clearInterval(times)
      times = setInterval(function () {
          var onOff = true
          for (let attr in target) { 
              let now = parseInt(getPos(ele, attr))
              let speed = (target[attr] - now) / 10
              speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);
              if (now == target[attr]) {
                  onOff = true
              }
              ele.style[attr] = now + speed + 'px';
          }
          for (var tip in target) {
              if (target[tip] !== parseInt(getPos(ele, tip))) {
                  onOff = false;
                  break;
              }
          }
          if (onOff) {
              clearInterval(times);
              cb && cb();
          }
      }, 30)
  }
```
**这个代码封装的是什么并不重要, 你不用着急仔细看他**
- 接下来就是调用了
![](./asset/01/image006.gif)

- 好了, 问题出现了, 怎么解决呢 ?
  + 我们只能是去读一读代码了, 只要把这个代码阅读明白了, 什么都解决了

### TS
- 这个时候, TypeScript 就可以排上用场了
- TypeScript 简称 TS
  -	就是在 JS 代码的基础上, 给每一个数据添加了一个数据类型限制
  - 在开发阶段, 可以提示你某个位置需要一个什么类型的数据
  - 在开发阶段, 当你给出的数据类型不对的时候, 可以及时提示你的错误
  - 在开发阶段, 你需要给出的数据少了或者类型错误, 会有提示出现
- 再来看一个 TS 的例子吧
  +	还是一段简单的代码
```js
  function and(a: number, b: number): number {
      return a + b
  }
```
**看不懂没关系, 暂时不需要你看懂, 别看他, 一会再说 **
-	接下来看看调用的时候会出现什么 
  + 注意: 编辑器代码中带有红色波浪线的表明代码中有报错


![](./asset/01/image009.gif)

![](./asset/01/image010.gif)

![](./asset/01/image011.gif)

![](./asset/01/image012.gif)



- 	这就是用 TS 写的一段代码, 我们会发现, 我都不需要去运行代
码, 不需要去查看结果, 在开发过程中, 就能通过编辑器给你提示出错误


![](./asset/01/image013.gif)


- 那么这样的话, 我岂不是可以才**开发过程中**避免很多错误, 而且很多时候我多不需要去特意记一些函数的参数类型了, 反正写错了编辑器会给我提示, 到时候我再看一下错误提示不就知道了,**这就是TypeScript**

- 百度百科介绍
  + TypeScript 是微软开发的一个开源的编程语言,$\color{red}{通过在 JavaScript 的基础上添加静态类型定义构建而成}$. TypeScript 通过 TypeScript编译器 或 Babel 转译为 JavaScript 代码,可运行在任何浏览器,任何操作系统

### 初体验
- 说了半天, 接下来, 我们就写一段 TS 运行起来试试看,可是浏览器只能执行js代码,所以需要有一个TS 编译器可以将TS代码编译为浏览器能执行的代码,但是TS的编译器不是自带的,需要咱自己单独安装
#### 安装 TS 编译器
  + 浏览器是不能直接运行 TS 代码的, 我们需要用工具, 把你写好的 TS 代码编译成 JS 代码, 放在浏览器内运行
  + 安装 TS 编译器
  + 直接使用 npm 安装全局 ts 工具即可 
    - windows: `npm install --global typescript`
    - MAC: `sudo npm install --global typescript`

#### 编译 TS 代码
- 接下来书写一段代码, TS 代码写在一个 .ts 后缀的文件内
```ts
  // index.ts 文件
  function sayHi(name) {
      console.log(`Hello, My name is ${ name }`)
  }
  sayHi('leon')
```
- 打开命令行开始编译就好了
  + `tsc index.ts`
  + 会将 index.ts 文件进行编译, 编译后生成同名 js 文件, index.js
  + 这里我们暂时没有写 ts 的内容, 只是按照 js 的代码在书写
- 每次修改原始 ts 文件, 都需要重新编译一遍, 好麻烦的
- 我们可以使用 --watch 指令来监控文件变化
  + `tsc --watch index.ts`
  		会实时监控 index.ts 文件内的变化, 只要代码发生改变, 会自动进行重新编译
- 编译 TS 成功 ? 失败 ? 
  + 咱们在代码内加入一点 ts 相关的内容, 再来编译试试看  
  ```ts
    // index.ts 文件
    // TS 的含义: 把这个 name 参数限制为只能是 string 类型数据
    function sayHi(name: string) {
        console.log(`Hello, My name is ${ name }`)
    }
    sayHi('leon')
  ```
  + 执行编译, 我们发现编译完全没有问题 


- 稍微做出一些修改, 我们再来一次
  ```ts
    // index.ts 文件
    // TS 的含义: 把这个 name 参数限制为只能是 string 类型数据
    function sayHi(name: string) {
        console.log(`Hello, My name is ${ name }`)
    }
    sayHi(1024)
  ```
  + 依旧是执行编译, 我们会发现编译器报错了
  ![](./asset/01/image023.gif)
  + 会告诉我们, 一个 number 类型的参数不能赋值给 string 类型
  + 这我能理解
  + 但是仔细看一下目录内的内容, 我发现, 依旧正常编译了一个 index.js 文件出来
  + 并且里面代码也是正常的, 没有问题的
  + 我到底是成功了 ? 还是失败了呢 ? 
- 分析一波
  + 上面的代码在 ts 内解析的含义是限制了 name 这个形参的数据类型必须是 string 类型
  + 主要你传递别的类型的数据, 就会报错, 但是这个类型错误, 也就是 ts 的错误
  + 所以在编译的过程中, 会提示你, 你的类型出现了错误
  + 但是不管你传递的实参是什么, 编译后的 js 代码是这样的
  ```js
    // index.js 文件
    function sayHi(name) {
        console.log(`Hello, My name is ${ name }`)
    }
    sayHi(1024)
  ```
  +	从 js 的角度来看,  这就是一段合法的代码
  		所以会成功编译出一个 js 文件

#### 小结
- 当你在书写 ts 的时候, 只要你的语法没有错误, 就会编译出一个 js 文件
- ts 只是在编译的过程中, 检测 并 提示 你数据类型是否出现了错误
- JavaScript 
  + 弱类型脚本语言
  + 对于数据类型没有任何限制
- TypeScript
  + 在 JS 的基础上, 加上了类型限制
  + 也就是一个强类型限制脚本语言, 浏览器不能识别, 需要编译成 js 来运行



## 二、TS基础类型
- 上面, 我们讲了 TS 的编译和初步使用
- 现在我们就开始正式进入 TS 的学习之旅
### 基础类型
- 我们先来对我们最基础的数据类型进行一些限制

#### 布尔类型
```ts
  let boo: boolean = false
```
- 当前这个 boo 变量的数据类型被限制为了 布尔类型
- 一旦将来给这个变量赋值的时候, 只要不是布尔类型, 就会提示你类型错误
![](./asset/02/image004.gif)

#### 数值类型
- ts 内的 number 类型都是按照浮点数存储的, 同时也支持十六进制, 八进制, 二进制等其他进制表示
```ts
  let num: number = 6
  num = 0xf00d
  num = 0b1010
  num = 0o744
```
-	给 num 变量限制为了 number 类型, 只要你给 num 赋值的是 number 类型数据就没问题, 其他不行
![](./asset/02/image006.png) 

#### 字符串类型
```ts
  let str: string = 'leon'
```
- 给 str  变量限制为了 string 数据类型
![](./asset/02/image008.png)

#### 多个基础类型
- 我们也可以通过 ( | ) 来给一个变量设置多个数据类型
```ts
  let foo: string | boolean = 'leon'
```
- 这个 foo 变量就被限制为 string 或者 boolean 类型的数据, 可以接受这两种数据类型 
- 课堂练习
	-  定义一个函数 calculate，它接受两个参数和一个操作符，并返回计算的结果。为了确保参数类型正确，我们将使用类型注解来限定参数只能是数字，并且操作符只能是一些预定义的字符串（如 '+', '-', '*', '/'）。
### 数组类型
#### 定义方式1
```ts
  const list: number[] = []
```
- 定义了一个 list 变量, 限制为一个数组的同时, 这个数组只能接受 number 数据
![](./asset/02/image011.gif) 
#### 定义方式2
```ts
  let list: Array<number> = [100, 200]
```
- 这种方式是采用的泛型的方式进行定义, 泛型后面我们会详细说
![](./asset/02/image013.gif) 

- 这种方式定义的数组, 也可以让数组内包含多种数据类型
```ts
  const list: Array<number | string> = [100, 200]
```
- 表示这个数组内可以添加 number 或者 string 类型的数据 
![](./asset/02/image015.gif) 

### 元组类型
#### 基础定义
- 元组( Tuple ) :  是 TS 中给出的一个概念, 其实就是一个已知元素数量和数据类型的数组
  + 元组是 TS 的一个概念, 在 JS 内没有元组这个概念
  + 在 JS 中
    + 数组是不限制长度的, 可以随意添加多少数据
    + TS 的元组, 编译以后, 其实就是 JS 中的数组 
    + 所以是不会被真正限制长度的
  + 在 TS 中
    - 元组也只是一个形式上的 已知元素数量 和 数据类型 的数组
    - 不是说超过限定长度就会报错
    - 只是通过元组的方式, 建议你该数组的长度和类型
  + 毕竟 TS 也只是在开发中给 JS 的各种数据添加上类型限制而已
```ts
  const list: [ number, string ] = [ 100, 'hello' ]
```
- 将 list 限定为一个元组
  + 该元组建议有两个数据
  + [0] 位置数据是一个 number 类型数据
  + [1] 位置数据是一个 string 类型数据
  + 初始化的时候, 就必须直接赋好值
![](./asset/02/image017.gif) 
		一定要注意一个问题, 就是元组的值顺序不能变
![](./asset/02/image018.gif) 

#### 可选值
-	我们可以使用 问号( ? ) 来决定某个值为选填项 
```ts
  const list: [ number?, string? ] = []
```
- 这个时候就是对 number 和 string 数据做了一个选填限制
- 该索引对应位置可以有值可以没有值
  - 但是一定要注意, 顺序不能变哦 

#### 元组越界
- 刚才我们说了, 元组其实本质上还是数组
  - 数组其实是没有长度限制的
  - 所以元组只是建议你不要超出长度, 但是其实超出去也没事
- 所以超出限制长度的数据, 就不会有过多的限制了
  - 你所以写的数据类型都可以
```ts
  const list: [ number, string ] = [ 100, 'hello' ]
  list.push(100)
  list.push(200)
  list.push('hello')
  list.push('world')
```
- 主要不在初始化的时候, 给出越界数据, 后面可以向数组里面追加数据
- 而且追加出来的多余的数据, 可以是 number 类型, 也可以是 string 类型
- 并且也没有了顺序的限制
- 但是其他数据类型还是不行
![](./asset/02/image021.gif) 

### Any 类型
- 有些时候, 我们对于某个数据, 没有办法确定是什么类型, 因为数据源可能是来自用户输入, 或者某些第三方库得来的, 所以我们没办法在一开始限制其数据类型
- 但是从 TS 的角度上来说, 每一个数据都要限制一次数据类型
- 所以, 给出了一个 Any(任意类型)
```ts
  let foo: any = 100
  foo = true
  foo = 'hello'
```
- foo 这个变量可以接受任何数据类型, 就相当于没有限制
- 但是对于一个严谨的程序员来说, 还是不建议经常性的使用 any, 因为这样的话 TS 的意义就不在了
![](./asset/02/image023.jpg) 


### 空类型
#### void
- 是一个和 any 类型刚好完全相反的类型, 它表示什么都没有
- 我们可以给一个变量设置为 void 类型, 但是没有人会这么做, 因为没有任何意义
```ts
  let foo: void = undefined
```
- 当你给 foo 设置为 void 类型以后, 这个变量就**只能接受 undefined 和 null 类型**数据了
- 其他的都不行
- void 还有一个地方就是用在 函数的返回值
  - 当这个函数没有返回值的时候, 你见到的类型限制就会是 void
```ts
  function and(a, b): void {
      console.log(a + b)
  }
```
- 当然, 我们也可以倒推这个结果
- 也就是说, 当你给一个函数的返回值设置为 void 以后
- 那么这个函数就不能写返回值了 
![](./asset/02/image026.gif) 

#### Never
-  这个类型表示的是那些永不存在的值的类型, 应用的地方相对比较少
-  一般如果用 Never 去描述一个函数的返回值, 那么这个函数就不能有任何返回出现, 也就是说这个函数必须不能正常结束, 所以我们就需要在该函数内让函数代码报错, 就是手动抛出异常, 或者让函数永不结束
```ts
  function fn(): never {
      throw new Error('出错啦')
  }
```
```ts
  function fn(): never {
       while (true) {}
  }
```


#### Undefined 和 Null
- 他们两个和 void 很像, 本身在 TS 内用处不是很大
- 分别对应 undefined 和 null 两个数据, 一般用不到 
```ts
  let u: undefined = undefined
  let n: null = null
```
- 但是 **undefined 和 null 可以作为任何类型的子类型出现**
- 也就是你设置其他类型, 也可以填写 undefined 或者 null 
```ts
  let n: number
```
- 此时 n 被限制为 number 类型, 但是目前 n 的值是 undefined, 也没有问题
- 因为 undefined 可以是 number 的子类型

### object 类型
- 这是一个特殊的类型限制, 不仅仅是代表 对象数据类型
- 表示的是 非基础数据类型 以外的所有类型
- 也就是除number，string，boolean，symbol，null 或 undefined 之外的类型
```ts
  let foo: object = 100
  foo = []
```
![](./asset/02/image032.gif) 

