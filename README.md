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
ngrok http 127.0.0.1:8080 -host-header="127.0.0.1:3030"
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