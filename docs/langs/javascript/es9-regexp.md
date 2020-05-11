# RegExp拓展

### 后行断言

​	**`后行断言`**也叫做**`零宽度正回顾后发断言`**。

#### (?<=y)x

​	**`零宽度正回顾后发断言`**，也叫**`反向肯定预查`**。是**`非捕获匹配`**，x只有在y后面才会被匹配。

```javascript
let s1 = '123alice'
let s2 = '456alice'
let s3 = '789alice'

let reg = /(?<=123|456)alice/ // 只有当alice前面是123或者456才匹配，否则不匹配

reg.test(s1) // true
reg.test(s2) // true
reg.test(s3) // false
```

---

#### (?<!y)x

​	**`零宽度负回顾后发断言`**，也叫**`反向否定预查`**。是**`非捕获匹配`**，x只有不在y后面才会被匹配。

```javascript
let s1 = '123alice'
let s2 = '456alice'
let s3 = '789alice'

let reg = /(?<!123|456)alice/ // 只有当alice前面不是123或者456才匹配，否则不匹配

reg.test(s1) // false
reg.test(s2) // false
reg.test(s3) // true
```

