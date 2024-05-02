## Vue框架安装

1.先去[官网](https://nodejs.org/en)下载nodejs，然后下一步下一步安装到（自建）NodeJs文件夹

2.再cmd输入命令检查是否成功

```
node -v
```

3.在cmd管理员模式下配置全局路径（之前就没有配置，导致只有一个文件夹有Vue环境）

```
npm config set registry ".....\NodeJs"
```

4.在cmd管理员模式下更换下载源

```
npm config get registry https://registry.npm.taobao.org/
```

## 创建Vue项目

第一种：在要创建项目的文件夹下输入cmd打开命令窗口，再输入

```
npm init vue@latest
```

第一次使用会先下载东西，等待即可

```
  cd vue-project  打开项目
  npm install     下载所需环境
  npm run dev     运行
```



第二种：（可能需要这步）打开cmd先下载Vue脚手架

```
npm install -g @vue/cli
```

然后输入命令，打开图形化创建项目界面

```
vue ui
```

