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

##ngrok

**ngrok dial tcp: lookup localhost: no such host**

描述：直接在命令行运用`./ngrok 3030`不能直接将线上服务器连接到本地服务器

解决：运行方式改为：
```bash
ngrok http 127.0.0.1:8080 -host-header="127.0.0.1:3030"
```

---

##other

**Provisional headers are shown**

描述：项目html加入img图片就会出现这样的报错，最后排查是Adblock插件屏蔽了该请求

解决：关闭Adblockc插件

