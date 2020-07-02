# 安装sass

### Mac安装Sass

```bash
# 通过 gem 安装
$ gem install sass

# 如果遇到权限问题
$ sudo gem install sass

# 查看是否安装成功
$ sass -v
```



### 将sass编译为css

```bash
# 普通编译
$ sass sass/style.scss:css/style.css

# 自动编译:监听单个文件
$ sass --watch sass/style.scss:css/style.css

# 自动编译:监听整个目录
$ sass --watch sass:css
```