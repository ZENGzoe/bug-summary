# bug 记录

---

## bash Error

**Error: EACCES: permission denied**

描述：用户无对该文件的功能权限，如node_modules的权限为root,其他用户无法该目录下的文件进行操作

解决：用命令`chown`修改文件权限，`chown`命令可以修改文件的拥有者。
1.可通过`ll`可查看当前目录下的文件权限
```bash
ll 
```
2.修改权限
`-R` 对指定目录下的所有文件和子目录进行相同的拥有者变更
```bash
sudo chown -R 变更后的用户名: ./node_modulesv
```

**Error: getaddrinfo ENOTFOUND localhost**

描述：启动webpack，未在启动项加上localhost的地址

解决：
在`webpack.config.js`的启动项加上：
```javascrit
"start": "webpack-dev-server --mode development --port 3030 --host 0.0.0.0 --content-base dist/",
```

---

## ngrok

**ngrok dial tcp: lookup localhost: no such host**

描述：直接在命令行运用`./ngrok 3030`不能直接将线上服务器连接到本地服务器

解决：运行方式改为：
```bash
ngrok http 127.0.0.1:3030 -host-header="127.0.0.1:3030"
```

---

## other

**Provisional headers are shown**

描述：项目html加入img图片就会出现这样的报错，最后排查是Adblock插件屏蔽了该请求

解决：关闭Adblockc插件

---

## Sublime text

**Apparent recursion within a with_prototype action: 25000 context sanity limit hit**

描述：打开Sublime Text弹出该错误弹窗

解决：升级Sublime Text

## Vue

**打开chrome dev tool无法使用vue调试插件**

描述：
无法使用vue调试插件分两种情况：
1.右上角vue logo为灰色
2.右上角vue logo变量，显示Vue.js is detected on this page. Open DevTools and look for the Vue panel，但chrome dev tool没有显示vue插件

解决：
1.项目运行环境不为production环境才能使用vue调试插件
2.如在运行模式非production环境，请确定是否使用了vue.min.js，使用vue.min.js为production环境
3.使用Vue.config.devtools = true可开启vue调试插件
4.进行以上操作后chrome dev tool仍无vue插件显示，请关闭重启chrome dev tool

## Node.js

**Converting circular structure to JSON**

描述：在路由内请求其他接口的数据，将返回的数据返回路由时，保此错

解决：
应直接返回数据，而且请求的promise，如res.data

## Git

**refusing to merge unrelated histories**

描述：当本地项目绑定远程仓库后，pull远程代码时，拉取失败，且提示该错误。

解决：当新绑定远程仓库，本地项目历史代码和远程仓库的历史代码不相同，需要手动同意不同历史代码合并

```bash
git pull origin master --allow-unrelated-histories
```

**Authentication failed. You may not have permission to access the repository. Open options and verify that you're signed in with an account that has permission to access this repository**

描述：在Github Desktop提交新项目代码时，提交失败，且提示该错误。

解决：由于在本地未给github设置ssh，因此设置中不能使用ssh提交代码，应用https地址

Github Desktop -> Repository -> Repository Settings -> Remote Repository URL 改为https的地址

## Hexo

**全局安装hexo-cli时安装失败，提示no such file or directory, chmod '/usr/local/lib/node_modules/hexo-cli/node_modules/atob/bin/atob.js**

描述：用户权限问题导致无法安装

解决：

设置用户的npm权限

```bash
npm config set user 0
npm config set unsafe-perm true
npm install -g hexo-cli
```

**No layout: index.html**

描述：运行`hexo s`预览页面白屏，并且命令窗口显示No layout: index.html

解决：博客主题配置错误或是主题package丢失的原因。可直接下载主题package到本地，复制到内容到`/themes/{主题包名}/`下。

## Sequelize.js

**1.Error: Please install mysql package manually**

描述：初始化数据库时无法初始化，提示需安装mysql

解决：

需要全局安装mysql

```
npm install mysql -g
```

## MySQL

**1.Client does not support authentication protocol requested by server; consider upgrading MySQL client**

描述：数据库连接失败

解决：密码错误，需要更改密码

（1）更改加密方式
```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;
```

（2）更改密码
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123';
```

（3）刷新
```
FLUSH PRIVILEGES;
```
