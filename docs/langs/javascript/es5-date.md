# Date对象

### 创建一个日期对象

创建一个新**`Date`**对象的唯一方法是通过**`new`**操作符。

> 语法：
>
> ```js
> // 根据当前本地时间创建一个日期对象
> new Date()
> 
> // 根据某个日期创建一个日期对象
> new Date(dateString)
> 
> // 或者
> new Date(year, MonthIndex[, day[, hours[, minutes[, seconds[, milliseconds] ] ] ] ] )
> ```
>

```javascript
var date = new Date() // 当前本地时间

// 方式1:月份可以写单词，最少三个字母
var date = new Date('Jul 8, 2018, 23:05:32') // Sun Jul 08 2018 23:05:32 GMT+0800 (中国标准时间)

// 方式2:日期和时间用T隔开，月日均为2位数
var date = new Date('2018-07-08T23:05:32') // Sun Jul 08 2018 23:05:32 GMT+0800 (中国标准时间)

// 方式3: 该种方式月份会加1
var date = new Date(2018, 06, 08, 23, 05, 32) // Sun Jul 08 2018 23:05:32 GMT+0800 (中国标准时间)
```

---

### 方法

#### ☂  Date.now()

​	返回自1970年1月1日 00:00:00 UTC到当前时间的毫秒数。

> 语法：
>
> ```js
> var timeInMs = Date.now()
> ```
>

```javascript
var timeInMs = Date.now() // 返回自1970.1.1 0:0:0到现在的毫秒值

// 兼容
if (!Date.now) {
	Date.now = function now() {
		return new Date().getTime()
	}
}
```

---

#### Date.parse()

​	解析一个表示某个日期的字符串，并返回从1970-1-1 00:00:00 UTC 到该日期对象（该日期对象的UTC时间）的毫秒数，如果该字符串无法识别，或者一些情况下，包含了不合法的日期数值（如：2015-02-31），则返回值为NaN。

> 语法：
>
> ```css
> Date.parse(dateString)
> ```
>

```javascript
Date.parse(2018, 6, 8, 23, 56, 54) // 1514764800000 (Number)
```

---

#### getTime()

​	返回一个时间的格林威治时间数值，表示从1970年1月1日0时0分0秒（UTC，即协调世界时）距离该日期对象所代表时间的毫秒数。

> 语法：
>
> ```css
> date.getTime()
> ```
>

```javascript
var howlong = date.getTime() // 返回自1970.1.1 0:0:0到现在的毫秒值
```

---

#### getTimezoneOffset()

​	返回协调世界时（UTC）相对于当前时区的时间差值，单位为分钟。

> 语法：
>
> ```css
> date.getTimezoneOffset()
> ```
>

```javascript
var x = new Date() // 本地时间
var currentTimezoneOffsetInhours = x.getTimezoneOffset() // 世界时 - 本地时间
```

---

#### toString()

​	返回一个字符串，表示该**`Date`**对象。

> 语法：
>
> ```css
> date.toString()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.toString() // 'Wed Nov 20 2019 05:33:24 GMT+0800 (中国标准时间)'
```

---

#### toTimeString()

​	以人类易读形式返回一个日期对象时间部分的字符串，该字符串以美式英语格式化。

> 语法：
>
> ```css
> date.toTimeString()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.toTimeString() // '05:33:24 GMT+0800 (中国标准时间)'
```

---

#### toDateString()

​		以美式英语和人类易读的形式返回一个日期对象日期部分的字符串。

> 语法：
>
> ```css
> date.toDateString()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.toDateString() // 'Wed Nov 20 2019'
```

---

#### toLocaleTimeString()

​	返回该日期对象时间部分的字符串，该字符串格式因不同语言而不同。

> 语法：
>
> ```css
> date.toLocaleTimeString()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.toLocaleTimeString() // '上午5:33:24'
```

---

#### toLocaleDateString()

​	方法返回该日期对象日期部分的字符串，该字符串格式因不同语言而不同。

> 语法：
>
> ```css
> date.toLocaleDateString()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.toLocaleDateString() // '2019/11/20'
```

---

### 获取本地时间

#### getFullYear()

​	根据本地时间，返回一个指定的日期对象的年份。

> 语法：
>
> ```css
> date.getFullYear()
> ```
>

```javascript
var year = date.getFullYear() // 年
```

---

#### getMonth()

​	根据本地时间，返回一个指定的日期对象的月份，为基于0的值（从0 -- 11，0表示一年中的第一月）。

> 语法：
>
> ```css
> date.getMonth()
> ```
>

```javascript
var month = date.getMonth() // 月
```

---

#### getDate()

​	根据本地时间，返回一个指定的日期对象为一个月中的哪一日（从1 -- 31）。

> 语法：
>
> ```css
> date.getDate()
> ```
>

```javascript
var day = date.getDate() // 日
```

---

#### getDay()

​			根据本地时间，返回一个具体日期中一周的第几天（从0 -- 6，0 表示星期天）。

> 语法：
>
> ```css
> date.getDay()
> ```
>

```javascript
var week = date.getDay() // 星期
```

---

#### getHours()

​	根据本地时间，返回一个指定的日期对象的小时（从0 -- 23）。

> 语法：
>
> ```css
> date.getHours()
> ```
>

```javascript
var hours = date.getHours() // 时
```

----

#### getMinutes()

​	根据本地时间，返回一个指定的日期对象的分钟数（0 -- 59）。

> 语法：
>
> ```css
> date.getMinutes()
> ```
>

```javascript
var minutes = date.getMinutes() // 分
```

---

#### getSeconds()

​	根据本地时间，返回一个指定的日期对象的秒数（0 -- 59）。

> 语法：
>
> ```css
> date.getSeconds()
> ```
>

```javascript
var seconds = date.getSeconds() // 秒
```

---

#### getMilliseconds()

​	根据本地时间，返回一个指定的日期对象的毫秒数（0 -- 999）。

> 语法：
>
> ```css
> date.getMilliseconds()
> ```
>

```javascript
var ms = date.getMilliseconds() // 毫秒
```

---

### 获取世界时

#### getUTCFullYear()

​		以世界时为标准，返回一个指定的日期对象的年份。

> 语法：
>
> ```css
> date.getUTCFullYear()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCFullYear() // 2019
```

---

#### getUTCMonth()

​	以世界时为标准，返回一个指定的日期对象的月份，它是从 0 开始计数的（0 代表一年的第一个月）。

> 语法：
>
> ```css
> date.getUTCMonth()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCMonth() // 10

var date2 = new Date('2019-11-20T20:33:24')
date2.getUTCMonth() // 10
```

---

#### getUTCDate()

​	以世界时为标准，返回一个指定的日期对象为一个月中的第几天。

> 语法：
>
> ```css
> date.getUTCDate()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCDate() // 19
```

---

#### getUTCDay()

​	以世界时为标准，返回一个指定的日期对象为一星期中的第几天，其中 0 代表星期天。

> 语法：
>
> ```css
> date.getUTCDay()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCDay() // 2
```

---

#### getUTCHours()

​	以世界时为标准，返回一个指定的日期对象的小时数。

> 语法：
>
> ```css
> date.getUTCHours()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCHours() // 21
```

---

#### getUTCMinutes()

​	以世界时为标准，返回一个指定的日期对象的分钟数。

> 语法：
>
> ```css
> date.getUTCMinutes()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCMinutes() // 33
```

---

#### getUTCSeconds()

​	以世界时为标准，返回一个指定的日期对象的秒数。

> 语法：
>
> ```css
> date.getUTCSeconds()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCSeconds() // 24
```

---

#### getUTCMilliseconds()

​	以世界时为标准，返回一个指定的日期对象的毫秒数。

> 语法：
>
> ```css
> date.getUTCMilliseconds()
> ```
>

```javascript
var date = new Date(2019, 10, 20, 05, 33, 24)
date.getUTCMilliseconds() // 0
```

