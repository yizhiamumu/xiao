# 一只阿木木


===
[预览](https://yizhiamumu.github.io/xiao/public/)
===


### 使用

1. 安装Node.js环境：https://nodejs.org/

2. 安装git: https://git-scm.com/

3. 执行以下命令：

``` bash
git clone https://github.com/yizhiamumu/xiao.git
cd xiao
npm install
npm run dev
```

### 部署

1. 编辑 config/index.js，修改第 10 行的 assetsPublicPath，值为 `项目名/public`。

	如果你没有修改项目名 xiaoshu，则可跳过此步骤。

2. 编译、上传
    
``` 
bash
npm run build
git add .
git commit -m "update"
git push
```

3. 开启 GitHub Pages 功能, 或者，把生成的目标文件```public/*```放在你的web服务器上。

