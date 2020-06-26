# oneindex
Onedrive Directory Index

鉴于大家issue里的追问和国际版速度的确很渣，这次来了大版本更新

# office A1账号免费获取

https://office.shax.vip

## Attention
 - 注意不管是之前的魔改还是非魔改版本，请拉取本程序重新安装下，因为token缓存换到redis里了！
 - 注意请先配置graph api或者在azure Application里配置好回调地址：https://tui.echoteen.com/api/office/serve

## 预览地址
http://pan.shax.vip

## 更新信息

- 2020-05-01
  - 修复redis连接判断
  - 实验性功能，支持sharePoint 个人反代或者cdn支持，加快国际版速度
  - 修改重定向地址为https://tui.echoteen.com/api/office/serve
  - 增加redis配置和cdn配置在安装中可配置

- 2019-01-08
  - 修复部分用户出现安装成功后无内容的bug
  - 优雅token缓存周期，无需定时任务，智能获取，优化数据缓存
  - 修改默认主题，修复图床上传问题，前提是你要打开图床
  - base.php里只涉及用户侧数据，去除refresh_token等，添加redis密码配置信息
  - 修改issue里bug

## 魔改说明：
- 感谢大佬donwa提供原版的oneindex源码

- 本代码大部分基于donwa的oneindex添加内容自用

## 魔改内容
- 缓存和token获取使用redis ,无需使用命令设置定时任务，增加默认有效期  

- 如果onedrive有上传或者删除文件，请后台手动清除缓存

- 图床使用ajax获取，可以直接展现链接和引用代码

## 功能：
不用服务器空间，不走服务器流量，  

直接列onedrive目录，文件直链下载。  

## demo
[https://xn.tn](https://xn.tn)  

## change log:  
18-03-29: 更新直链获取机制、缓存机制，避免频繁访问的token失效  
18-03-29: 解决非英文编码问题  
18-03-29: 添加onedrive共享的起始目录 功能  
18-03-29: 添加rewrite的配置文件  
18-03-29: 增加sqlite模式cache支持  
18-03-29: 添加缩略图功能  
18-03-29: 添加404判断  
18-03-31: 添加console  
18-04-13: 修复特殊文件名无法下载问题  
18-04-13: 添加命令行上传功能  
18-04-16: 更新 2.0 beta  
18-04-16: 更新展示界面  
18-04-16: 响应式，支持小屏设备  
18-04-16: 图片在线预览  
18-04-16: 视频在线播放  
18-04-16: 代码在线查看（js、css、html、sh、php、java、md等）  
18-04-16: README.md 支持，解析各目录下(onedirive目录下) README.md 文件，在页面尾部展示。  
18-04-18: 音频在线播放  
18-04-18: HEAD.md 支持，在页面头部展示   
18-04-18: .password 文件夹加密  
18-05-06: 在线视频播放器替换成 Dplayer  
18-05-06: 在线视频播放支持'mp4','webm','avi','mpg', 'mpeg', 'rm', 'rmvb', 'mov', 'wmv', 'mkv', 'asf'  
18-06-01: 支持个人账号  
18-06-01: cli文件夹上传（单线程）  
18-06-01: 管理后台(后台地址:?/admin 默认密码:oneindex)  
18-06-01: 不同后缀展示设置  
18-06-01: 文件直接输出  
18-06-01: 文件上传管理（后台） 
18-06-01: 增加index.html特性   
18-06-01: 图床功能   

## 需求：
1、PHP空间，PHP 5.6+ 打开curl支持  
2、onedrive 账号 (个人、企业版或教育版/工作或学校帐户)  
3、oneindex 程序   

## 安装：
<img width="658" alt="image" src="https://raw.githubusercontent.com/donwa/oneindex/files/images/install.gif">  


## docker 安装运行：

从docker仓库获取镜像：
```sh
none
```

或者从源码构建镜像：

```shell
git clone https://github.com/david7207/oneindexMod.git
cd oneindex/
docker build -t your-image-name .
```

运行：

```shell
docker run -d -p {open port}:80 --name {container name} --restart=always {image name}
```

停止删除容器：

```shell
docker stop {container name}
docker rm -v {container name}
```

## 特殊文件实现功能  
` README.md `、`HEAD.md` 、 `.password`特殊文件使用  

可以参考[https://github.com/donwa/oneindex/tree/files](https://github.com/donwa/oneindex/tree/files)  

**在文件夹底部添加说明:**  
>在onedrive的文件夹中添加` README.md `文件，使用markdown语法。  

**在文件夹头部添加说明:**  
>在onedrive的文件夹中添加`HEAD.md` 文件，使用markdown语法。  

**加密文件夹:**  
>在onedrive的文件夹中添加`.password`文件，填入密码，密码不能为空。  

**直接输出网页:**  
>在onedrive的文件夹中添加`index.html` 文件，程序会直接输出网页而不列目录。  
>配合 文件展示设置-直接输出 效果更佳  

## 命令行功能  
仅能在php cli模式下运行  
**上传文件:**  
```
php one.php upload:file 本地文件 [onedrive文件]
```


**上传文件夹:**  
```
php one.php upload:folder 本地文件夹 [onedrive文件夹]
```

例如：  
```
//上传demo.zip 到onedrive 根目录  
php one.php upload:file demo.zip  

//上传demo.zip 到onedrive /test/目录  
php one.php upload:file demo.zip /test/  

//上传demo.zip 到onedrive /test/目录并命名为 d.zip  
php one.php upload:file demo.zip /test/d.zip  

//上传up/ 到onedrive /test/  
php one.php upload:file up/ /test/
```
