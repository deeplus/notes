# 安装



### 注意

​		在安装electron的时候，我们可以指定arch=ia32来安装32位的electron，在windows平台上打包都应该基于32位来打，这样打出来的包在32位和64位都可以用

```bash
$ npm install --arch=ia32 --platform=win32 elctron --save-dev
```

---

### 验证安装成功

```bash
$ npx electron -v
$ ./node_modules/.bin/electron -v
```

