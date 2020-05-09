# 改变git的ui样式

找到安装git的文件夹，进去之后，右击 `git-bash.exe` 选择以管理员身份运行 ，接着复制粘贴如下命令：

```bash
$ git clone https://github.com/xnng/my-git-bash.git
$ cd my-git-bash
$ git clone https://gitee.com/xnng/bash.git
$ cd bash
```

接下来，安装字体：

```bash
# 运行完下面这条命令之后，window电脑会打开两个文件夹(c://Windows/Fonts  /my-git-bash/bash/font)
# 一个文件里有很多.ttf文件，另一个文件里只有一个，把仅有的这一个直接拖到另一个有很多文件的文件夹里

$ start c://Windows//Fonts && start %cd%/fonts
```

接下来，安装主题：

```bash
$ cp .minttyrc ~ && cp git-prompt.sh /etc/profile.d
$ exit
```

做完上面的操作之后，有的电脑会重启一下 git-bash ，有的电脑把 git-bash 关了之后就不会再重启；如果电脑没有自动重启 git-bash ，只需要手动打开就可以。