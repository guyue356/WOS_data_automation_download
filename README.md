# Web of Science 论文数据自动化采集程序使用教程
## 1Selenium环境配置
### 1.1安装Chrome浏览器与对应版本的浏览器驱动
**①浏览器安装网址**：https://www.google.cn/chrome/<br>
**②浏览器驱动安装网址**：https://googlechromelabs.github.io/chrome-for-testing/<br>
**！！注意**：**驱动版本一定要与浏览器的大版本对应上**。通过Chrome浏览器“右上角竖三点→帮助→关于Google Chrome”可以查看当前浏览器版本。Chrome浏览器的版本更新较为频繁，如若不想频繁更新对应的新版本驱动，可以关闭自动更新，详见https://www.bilibili.com/video/BV1Y9UPYAEqN?spm_id_from=333.788.videopod.episodes&vd_source=e5b26c0088354e9a1dfee9f9a358d13c&p=2。
### 1.2下载第三方库
在CMD（终端）中运行`pip install selenium`
## 2运行程序
建议以jupyter notebook的形式直接运行文件，不要转化为python文件。（方便在程序中断时继续采集后续数据）
### 2.1启动浏览器
首先运行浏览器设置和启动浏览器两个模块,在打开的目标网页中跳转至检索链接。<br>
**当前的新版WOS很容易识别出Selenium，并弹出如图所示人机认证：**<br>
<img width="959" height="506" alt="image" src="https://github.com/user-attachments/assets/b342cc98-9d9d-47e7-a711-39208eeff8a3" />
<br>
该验证即使手动顺利通过，也无法进入目标数据库：<br>
<img width="959" height="509" alt="image" src="https://github.com/user-attachments/assets/765091f3-835a-468f-a6d5-74efd250485a" />
<br>
**如何绕过反爬**当前的WOS基本都能识别出Selenium
在打开的浏览器中输入需要爬取网站的检索链接
### 2.2文件路径设置

修改代码中
```
# 文件下载路径
downloads_path = Path("your download path")
#文件保存路径
save_path = Path(r"your path")
```

