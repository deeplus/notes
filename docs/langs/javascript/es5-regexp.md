# RegExp对象

​	正则表达式（Regular Expression）又被称为规则表达式，通常用来检索、替换那些符合某种模式（规则）的文本。



### 创建一个正则表达式

​	你可以使用以下两种方法之一构建一个正则表达式：

#### 字面量

​	使用一个正则表达式字面量，其由包含在斜杠之间的模式组成，**`字面量的参数不使用引号`**。

​		字面量形式，为正则表达式提供了的**`脚本加载后的编译`**（compilation），当正则表达式保持为**`常量`**时使用字面量。例如当你在循环中使用字面量构造一个正则表达式时，正则表达式不会在每一次迭代中都被重新编译（recompiled）。

​		使用正则表达式字面量为正则表达式提供了脚本加载后的编译。当正则表达式保持不变时，使用此方法可获得更好的性能。

> 语法：
>
> ```js
> var reg = /pattern/[flags]
> ```
>
> 参数：
>
> * **`parrern`**：正则表达式的文本；
>
> * **`flags`**(可选)：标识符；
>

```javascript
var rag = /abc/g
```

---

#### 构造函数

​	调用**`RegExp`**对象的构造函数，**`构造函数的参数要使用引号`**。

​		构造函数，为正则表达式提供了**`运行时的编译`**（runtime compilation）。如果你知道正则表达式模式将会改变，或者你事先不知道什么模式，而是从另一个来源获取，如用户输入，这些情况都可以使用构造函数。

> 语法：
>
> ```js
> var reg = new RegExp(pattern[, flags])
> ```
>

```javascript
var reg = new RegExp('abc', 'g')
```

---

### 属性

#### lastIndex

​	**`lastIndex`**是正则表达式的一个可读可写的整型属性，用来指定下一次匹配的起始索引。

​	使用全局标识符**`g`**之所以能够全局匹配，就是因为有**`lastIndex`**的存在。

```javascript
var str = 'aliceisalone'

var reg = /\d{4}/g;

console.log(reg.lastIndex, reg.test(str)) // 0 true

console.log(reg.lastIndex, reg.test(str)) // 6 true

console.log(reg.lastIndex, reg.test(str)) // 12 false

console.log(reg.lastIndex, reg.test(str)) // 0 true
```

---

### 方法

#### test()

​	执行一个检索，用来查看正则表达式与指定的字符串是否匹配。匹配返回 **`true`** 不匹配则返回 **`false`**。

> 语法：
>
> ```css
> reg.test(str)
> ```
>
> 参数：
>
> * **`str`**：用来与正则表达式匹配的字符串。
>

```javascript
/123/.test('1234567'); // true
/124/.test('1234567') // false
```

---

#### exec()

​	在一个指定字符串中执行一个搜索匹配，如果匹配**`成功`**返回一个**`数组`**（包含额外的属性 `index` 和 `input` ，并**`更新`**正则表达式对象的`lastIndex`属性，匹配**`失败`**则返回 **`null`**,并将 `lastIndex`的值**`重置`**为 `0`。

> 语法：
>
> ```css
> reg.exec(str)
> ```
>

```js

```

---

### 标识符

#### i

​	忽略大小写（ignore case）。

```javascript
('ALICE').match(/alice/); // null

('ALICE').match(/alice/i); // ["ALICE", index: 0, input: "ALICE", groups: undefined]
```

---

#### g

​	全局匹配（globe）。找到所有的匹配，而不是在第一个匹配后就停止。

```javascript
('ALICE').match(/\w/); // ["A", index: 0, input: "ALICE", groups: undefined]

('ALICE').match(/\w/g); // ["A", "L", "I", "C", "E"]
```

---

#### m

​		换行匹配。

```javascript
const str = 'hello\nword';

/^w/.test(str); // false

/^w/m.test(str) // true
```

---

### 元字符

​	所谓元字符就是指那些在**`正则表达式`**中具有特殊**`意义`**的专用字符，可以用来规定其前导字符（即位于元字符前面的字符）在目标对象中的出现模式。

#### 转义符( \ )

​	对于那些通常被认为字面意义的字符来说，表示下一个字符具有特殊用处，并且不会被按照字面意义解释。

```javascript
/*
* 	例如：b是一个普通字符，/b/表示匹配字符'b'，加上一个反斜杠，/\b/表示匹配一个单词边界。
*/
```

​	对于那些通常特殊对待的字符，表示下一个字符不具有特殊用途，会被按照字面意义解释。

```javascript
//	例如：*是一个特殊字符，表示匹配某个字符0或多次，/a*/意味着0或多个a，在它见面加上一个反斜杠，/a\*/表示匹配字符'a*'
```

---

#### .

​	匹配任意一个除行结束符（\n、\r、\u2018、\u2019）以外的字符。

```javascript
/.y/.test('yes make my day') // 匹配'yes make my day'中的'my'和'ay'，但不匹配'yes'
```

---

#### \d

​	匹配任意一个阿拉伯数字，等价于**`[0 - 9]`**。

```javascript
/\d/.test('123'); // true
```

---

#### \D

​	匹配任意一个不是阿拉伯数字的字符，等价于**`[^0 - 9]`**。

```javascript
/\D/.test('abc'); // true
```

---

#### \w

​	匹配任意一个基于拉丁字母表中的数字、字母、下划线。等价于 **`[A-Za-z0-9_]`**。

```javascript
/\w/.test('_proto'); // true
```

---

#### \W

​	匹配任意一个不是基本拉丁字母表中单词（字母、数字、下划线）字符的字符。等价于 **`[^A-Za-z0-9_]`**。

```javascript
/\W/.test('background-color'); // true
```

---

#### \s

​	匹配一个空白符，包括空格、制表符、换页符、换行符和其他 Unicode 空格。

```javascript
/\s/.test(''); // false
/\s/.test(' '); // true
```

---

#### \S

​	匹配一个非空白符。

```javascript
/\S/.test(''); // false
/\S/.test(' '); // false
/\S/.test('a'); // true
```

---

#### 其它

|    字符    |                含义                |
| :--------: | :--------------------------------: |
|  **`\r`**  | 匹配一个回车符（carriage return）  |
|  **`\n`**  |     匹配一个换行符（linefeed）     |
|  **`\f`**  |    匹配一个换页符（form-feed）     |
| **`[\b]`** |    匹配一个退格符（backspace）     |
|  **`\t`**  |     匹配一个水平制表符（tab）      |
|  **`\v`**  | 匹配一个垂直制表符（vertical tab） |

---

### 边界

#### ^

​	匹配字符串起始。

```javascript
/^a/.test('a An'); // true, 匹配'a An'中的'a'

/^A/.test('a An') // false，不匹配'a An'中的'A'
```

---

#### $

​	匹配字符串结束。

```javascript
/t$/.test('eat'); // true, 匹配'eat'中的't'

/t$/.test('eater') // false，不匹配'eater'中的't'
```

---

#### \b

​	匹配一个零宽单词边界（zero-width word boundary），即一个单词与一个空格之间的位置。

​		单词边界：包括单词起始、结束和连词符（除了\w之外的所有字符都属于连词符）。

```javascript
/\bn/.test('at noon'); //true, 匹配'noon'中的前一个'n'

/y\b/.test('possibly yesterday.') //true, 匹配'possibly'中的'y'
```

---

#### \B

​	匹配一个零宽非单词边界（zero-width non-word boundary），如两个字母之间或两个空格之间。

```javascript
/\Bn/.test('at noon'); //true, 匹配'noon'中的后一个'n'

/y\B/.test('possible yesterday.') //true, 匹配'yesterday.'中的第一个'y'
```

---

### 量词

​	当正则表达式存在量词时，默认是**`贪婪匹配(greedy)`**（即以最高次数匹配，如果不成功就依次降低次数，直到最低次）。

​		如果在量词的**`*`**、**`+`**、**`?`**、**`{}`**，任意一个后面紧跟**`？`**，就会使量词变为**`非贪婪模式(non-greedy)`**（以最低次数匹配，如果不成功就依次升高次数，直到最高次）。

!> 当要匹配的内容为**`数字`**，如果量词的**`左区间为0`**,那么就只能取到**`''`**。

```js
var str = 'zhenxi123456789';

/*
*		以下几种情况特殊：都取不到值
*		["", index: 0, input: "zhenxi123456789", groups: undefined]
*/
/\d{0,}/.exec(str);
/\d{0,1}/.exec(str);
/\d?/.exec(str);
/\d*/.exec(str);
```

---

#### x{m, n}

​	m，n均为正整数，前边的模式 x 至少出现m次、至多出现n次时匹配，**`注意不能有空格`**。

```javascript
var str = "zhenxi123456789"

// 默认贪婪模式
str.match(/\d{5,10}/g) // ["123456789"]

// 切换至非贪婪模式
str.match(/\d{5,10}?/g) // ["12345"]
```

---

#### x{m}

​	前面的模式x 出现m次时匹配。

```javascript
('caaaandy').match(/a{2,}/g) // ["aa"]，匹配前两个a
```

---

#### x*

​	前边的模式x至少0次，至多∞次时匹配，等价于**`x{0,}`**。

```javascript
('A ghost booooed').match(/bo*/g); // ["boooo"]

('A bird warbled').match(/bo*/g); // ["b", "b"]
```

---

#### x+

​		前边的模式x至少1次，至多∞次时匹配，等价于**`{1,}`**。

```javascript
('caaaaaaandy').match(/a+/g); // ["aaaaaaa"]
```

---

#### x?

​	前边的模式x 0次或1次时匹配，即可有可无，等价于**`x{0, 1}`**。

```javascript
('angel').match(/e?le?/g); // ["el"]

('angle').match(/e?le?/g); // ["le"]
```

---

### 子集

​	子集是指被**`()`**包裹的部分，表示被包裹部分是一个整体。

#### (x)

​	**`捕获匹配`**，匹配x并且捕获匹配项。**`捕获匹配`**意味着**`repalce()`**里的**`$n`**和**`子集`**里的**`\n`**能够生效。

```javascript
// 交换字符串中两个字符的位置

var str = '阳春白雪'

var reg = /(阳春)(白雪)/;
// 等价于
var reg = /([\D]{2})(\D{2})/g;
// 或者
var reg = /(.{2})(.{2})/g;
// 或者
var reg = /([\u4e00-\u9fa5]{2})([\u4e00-\u9fa5]{2})/g; // 推荐

str.replace(reg, '$2$1') // '白雪阳春'
```

---

#### \n

​	n是一个正整数，一个反向引用（back reference），指向正则表达式中第 n 个括号（从左开始数）中匹配的子字符串。例如：\1表示正则表达式的第一个括号，\2表示正则表达式的第二个括号，依次类推。

​		**`该用法必须在有子集的情况下才能生效`**

```javascript
var str = '111222233333'
var reg = /(\d)\1+/g;

str.match(reg) // ["111", "2222", "33333"]
```

---

#### {?:x}

​	**`非捕获匹配`**，匹配x但不捕获匹配项。**`非捕获匹配`**意味着**`repalce()`**里的**`$n`**和**`子集`**里的**`\n`**不会生效。

```javascript
var str = '11112345'
var reg = /(?:1111)/g

str.match(reg) // ["1111"]
```

---

### 范围词

!> 范围词里所有的字符串都是**`或者关系`**

```js
var reg = /alic[ey]/g;
// 匹配 alice 或者 alicy
```

!> 大部分具备特殊意义的符号（比如**`.`**、**`*`**、**`+`**等），在范围词里边，将不再具备特殊意义，而是会被当作普通字符处理，即使使用**`\`**也不行。

```js
var str = 'ab1*cd2'

str.match(/[.]/g); // null
str.match(/[\.]/g); // null

str.match(/[1*]/g); // ["1", "*"]
```

---

#### [xyz]

​	一个字符集合，也叫字符组。表示匹配到集合中的任意一个字符，也可以使用**`-`**指定一个范围。

> **`[0123456789]`** ：等价于**`[0-9]`**,也等价于**`\d`**；
>
> **`[abcd]`**: 等价于**`[a-d]`**
>
> **`[a-zA-Z0-9]`**：等价于**`\w`**

---

#### [^xyz]

​		一个反义或补充字符集，也叫反义字符组。表示匹配任意一个不在集合内的字符，也可以使用**`-`**指定一个范围。

```javascript
var str = 'abcd'
var reg = /[^abc]/g;
str.match(reg) // ["d"]
```

---

#### x|y

​	匹配x或y，表示左边所有或者右边所有。

```javascript
var reg = /alic(e|y|ing)/g;
// 匹配 alice 或者 alicy 或者 alicing
```

---

#### [\u4e00-\u9fa5]

​	匹配任意一个中文字符。

```javascript
var str = '阳春，白雪'

var reg = /[\u4e00-\u9fa5]/g

str.replace(reg, 'abc') // 'abcabc，abcabc'
```

---

### 先行断言

​	**`先行断言`**即**`零宽度正预测先行断言`**。

#### x(?=y)

​	**`零宽度正预测先行断言`**，也叫**`正向肯定预查`**，是**`非捕获匹配`**，仅匹配被y跟随的x。

```javascript
var s1 = 'alice123'
var s2 = 'alice456'
var s3 = 'alice789'
var reg = /alice(?=123|456)/g // 当alice后面跟123或者456则匹配，否则不匹配

reg.test(s1) // true
reg.test(s2) // true
reg.test(s3) // false
```

---

#### x(?!y)

​	**`零宽度负预测先行断言`**，也叫**`正向否定预查`**，是**`非捕获匹配`**，仅匹配不被y跟随的x。

```javascript
var s1 = 'alice123'
var s2 = 'alice456'
var s3 = 'alice789'

var reg = /alice(?!123|456)/ // 当alice后面跟的不是123或456时匹配，否则不匹配

reg.test(s1) // false
reg.test(s2) // false
reg.test(s3) // true
```



