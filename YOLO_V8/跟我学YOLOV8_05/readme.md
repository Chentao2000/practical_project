

# 在云GPU环境跑通YOLOV8并训练自己的数据集

> 如果没钱买中高端显卡，且不想背个超级重的游戏本，那你一定不要错过云GPU了！！
> 这东西会搞之后，你玩机器学习这类需要电脑算力的体验感直接成倍上升！就拿我那华为电脑的辣鸡英伟达显卡MX250 来说 ，哪怕云GPU最低配置一块钱一个小时的显卡，跑出来的速度都是我的五倍以上，且现在本身的云GPU非常成熟，已经配置好环境且一键备份，瞬间感觉到了解放生产力的力量！！
# 1. 下载VNC，后续要用它来连接镜像
VNC网址：https://www.realvnc.com/en/connect/download/vnc/
# 2. 进入云GPU
云GPU网址：[https://www.matpool.com/user/matbox](https://www.matpool.com/user/matbox)
这里我选用的是矩阵云 ，主要是看着界面简洁，同样的网站还有阿里云 腾讯云 亚马逊云 都差不多！
# 3. 注册登录云GPU
# 4. 充值（这次用到的是2块钱/小时的显卡）
![在这里插入图片描述](https://img-blog.csdnimg.cn/4525098608ee4b9ab9c323c65968972e.png)


# 5. 为了节省时间（钱），先把yolov8的文件夹压缩并添加到“我的网盘”
![在这里插入图片描述](https://img-blog.csdnimg.cn/267b6093ca4a4c78845ea62fe90cbcea.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/3c4ef23e5f47434a90e474dddd867bcd.png)
# 6.  点击左上角主机市场->GPU
![在这里插入图片描述](https://img-blog.csdnimg.cn/150c058e0ed343c9a8260326a47124d4.png)


# 7. 根据yolov8的需要选择适合的镜像
![在这里插入图片描述](https://img-blog.csdnimg.cn/855e62b2cfec43ca88fbff912b38b992.png)

<br>点进去选择镜像，yolov8一般需要至少两块钱一个小时的镜像环境
![在这里插入图片描述](https://img-blog.csdnimg.cn/e5e5f09dd1cb467ba30a67f83c5b7103.png)
# 8. 启动镜像

等待启动：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/5268a251732c444d9935b1628d371ca2.png)
<br>
运行中：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/813a8877e12a47d3a2d16c8cfe2a353e.png)
<br>
打开VNC并粘贴链接：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/9f3c516c4316403496a94f5c6afbbc48.png)
<br>弹出窗口按continue<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/c705270e22754a5cb4713b8b5e4ae7f6.png)
<br>
再粘贴密码：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/7dc157b9bf21463c896a5e4ed6d577c5.png)
<br>
就进入镜像啦<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/f93079f9f7694c2498f115a5736733a4.png)
# 9.打开数据集
1. 在桌面打开"我的网盘"解压文件<br>

![在这里插入图片描述](https://img-blog.csdnimg.cn/43b02dbeb96f4e1ba86cfa6cf6490252.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/7eb762646faf43c7a1daa3eddb4f7d76.png)
2. 打开pycharm
<br>打开项目<br>

![在这里插入图片描述](https://img-blog.csdnimg.cn/3efef10fcf8747aaa7c3eb59d3bc2cf5.png)
<br>这时项目在根目录如下路径中：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/24dd658ac3f746d59cd7b4ee6d3af46f.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/1e5f549998fd44b8865a59bac9e2d016.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d9bc7684ee9843a7b0a31ff605e45359.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/60f8156a47e441d597a760649b1454bd.png)
# 10、安装依赖
在终端中输入：

```python
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

```python
python setup.py install
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/36444ecf61dd4400b35ecd42d653b95b.png)
# 11、训练数据集

```python
yolo task=detect mode=train model=yolov8s-adding.yaml data=v8UAVdata/data.yaml epochs=100 imgsz=640 workers=4
```
开始训练：<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/b3e2565620ed4ecc9944448a75440e61.png)
# 12、导出数据
从云GPU环境中导出数据，需要把文件夹压缩成压缩包并放到“我的网盘”中，最后在windows的云GPU网页的“我的网盘”中下载
1. 先把需要下载的文件放到“我的网盘”中，再在“我的网盘”文件夹中打开终端，输入如下代码：<br>
（其中的newUAVtrain就是需要压缩的文件名称，自行修改）
```python
tar -czvf newUAVtrain.tar.gz newUAVtrain
```
2. 在windows网页的云GPU网页中找到我的网盘，就能看见压缩包并且下载了<br>
![在这里插入图片描述](https://img-blog.csdnimg.cn/d53c012b09d24f1386e7496007a7c326.png)



# 13、使用完后保存镜像
![在这里插入图片描述](https://img-blog.csdnimg.cn/88c277d554f34c13bf1ba12e518dbae2.png)

> 好啦 ！这就是 关于云GPU跑yolov8的全部教程，快点去试试吧！
