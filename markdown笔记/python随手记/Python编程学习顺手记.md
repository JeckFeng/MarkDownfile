# Python编程学习顺手记
### 如何快速安装多个依赖包

新建一个requirements.txt文件，文件内容为：<img src="C:\Users\fxl\AppData\Roaming\Typora\typora-user-images\image-20210507103744278.png" style="zoom:50%;" />
然后回到这个txt文件的目录下打开终端，运行命令：

```python
pip install -r .\requirements.txt
```

### 如何在当前文件夹下打开终端，而不是在win+R，输入cmd？

解决：在当前文件夹下按住shift的同时右键单击空白处，从菜单中选择＂在此处打开命令行窗口＂的项；

### pip下载超时如何解决？

解决：在pip后加上

```
-default-timeout=10000
```

 ，或者修改镜像源，在下载命令的最后加上

```
 -i https://pypi.douban.com/simple django
```

### pytorch错误

```python
RuntimeError: DataLoader worker (pid(s) 10792) exited unexpectedly

```

解决：num_workers 改为0 ，即不使用多线程