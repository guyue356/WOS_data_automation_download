# Web of Science 论文数据自动化采集程序使用教程
## 1Selenium环境配置
### 1.1安装Chrome浏览器与对应版本的浏览器驱动
**①浏览器安装网址**：https://www.google.cn/chrome/<br>
**②浏览器驱动安装网址**：https://googlechromelabs.github.io/chrome-for-testing/<br>
**！！注意**：**驱动版本一定要与浏览器的大版本对应上**。通过Chrome浏览器“右上角竖三点→帮助→关于Google Chrome”可以查看当前浏览器版本。Chrome浏览器的版本更新较为频繁，如若不想频繁更新对应的新版本驱动，可以关闭自动更新，详见https://www.bilibili.com/video/BV1Y9UPYAEqN?spm_id_from=333.788.videopod.episodes&vd_source=e5b26c0088354e9a1dfee9f9a358d13c&p=2。
### 1.2下载第三方库
在CMD（终端）中运行`pip install selenium`
## 2程序的运行
建议以jupyter notebook的形式直接运行文件，不要转化为python文件。（方便在程序中断时继续采集后续数据）
### 2.1启动浏览器
首先运行浏览器设置和启动浏览器两个模块,在打开的目标网页中跳转至检索链接。<br>
**当前的新版WOS很容易识别出Selenium，并弹出如图所示人机认证：**<br>
<img width="959" height="506" alt="image" src="https://github.com/user-attachments/assets/b342cc98-9d9d-47e7-a711-39208eeff8a3" />
<br>
该验证即使手动顺利通过，也无法进入目标数据库：<br>
<img width="959" height="509" alt="image" src="https://github.com/user-attachments/assets/765091f3-835a-468f-a6d5-74efd250485a" />
<br>
**如何绕过反爬**：在第2个模块打开的浏览器中手动新建一个网页，并进入目标链接，若弹出人机验证，则手动完成，待成功进入目标数据库后，再在第一个网页中打开目标链接，此时便已经绕过反爬，成功进入目标数据库。<br>
操作示例如下：<br>
①新建网页<br>
<img width="1920" height="1020" alt="ca75b407-71e6-448c-9ca1-37e95fbe9240" src="https://github.com/user-attachments/assets/3453c3a5-1f98-49c4-a46b-9384d485d078" />
<br>
②在新建网页中跳转至目标链接，并手动完成人机验证（若没有弹出人机验证，则说明没被识别出，可以直接下一步）<br>
<img width="1920" height="1016" alt="image" src="https://github.com/user-attachments/assets/8e5377ac-9d49-4fe7-ac3d-1e6c57858e5b" />
<br>
如图所示即为成功进入目标数据库：<br>
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/9e37753c-857b-4caf-993a-3fb90792f8b3" />
<br>
③在第一个网页中跳转至目标链接。
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/dec2e390-56e7-444a-b171-b519d7926e6e" />
<br>
**注意**:千万不要在成功进入目标数据库前，手动完成第一个网页的人机验证。因为通过程序打开的第一个网页受selenium控制，手动完成人机验证极容易被WOS识别出，导致目标数据库关闭，数据库关闭则需要重新运行该程序；而手动新建的第二个网页不受Selenium控制，可以骗过反爬，骗过反爬后，再使用受Selenium控制的第一个网页就不会弹出人机验证，可以直接进入要爬取的目标数据库完成后续数据采集任务。
### 2.2自动化导出步骤设计
进入数据库后运行模块`3.自动化导出的步骤设计`，该模块当前默认爬取“全记录与引用的参考文献”，若仅需要全记录，可以如图修改代码：<br>
<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/7f0f174e-1cb8-4871-8c88-df59c5c25d16" />
<br>
另外，WOS网页每过一段时间其元素定位可能会发生变化，若网页元素变更或有其他需求，可以自行更换Xpath定位，也可以联系作者进行维护。<br>
### 2.3自动化导出
①自动化导出配置<br>
**文件下载路径**：更换为网页默认的下载路径，如不清楚默认下载路径，可以手动下载一次，确定该路径。<br>
**文件保存路径**：更换为你想要保存的位置
<br>
示例如下：<br>
```
# 文件下载路径
downloads_path = Path(r"C:/Users/guyue/Downloads")
#文件保存路径
save_path = Path(r"C:\Users\guyue\Desktop\hsj\WHU\人工智能科研创新统计监测及比较研究\data\10_全领域\test")
```
**起始点**：修改起始点s，初始默认为1；当程序因为网络等问题被中断运行时，可以仅更换起始点，再次运行模块`4.自动化导出`，接着爬取后续数据。
<br>
③运行程序<br>
要采集全记录与引用的参考文献时，使用`4.1自动化导出（每次下载500条数据）`，该格式最多一次导出500条；全记录与其他类型的导出则可以使用`4.2自动化导出（每次下载1000条数据）`<br>
代码正常运行时如图所示：<br>
<img width="543" height="140" alt="image" src="https://github.com/user-attachments/assets/2910c9d0-8ff7-451e-91f1-b3fa1a97a839" />
<br>
**注意**每次运行`4.自动化导出`模块前，请检查默认文件下载路径中有没有名为"savedrecs.txt"的文件，如有请删除该文件，以确保文件保存时能够被正确命名。
<br>此外，当前WOS导出文件时可能会出现每导出10次就弹出人机验证的现象，该程序会等待150s，此时需要手动通过人机验证，便可确保程序正常运行，继续采集数据。
<br>若验证超时或网络超时导致程序中断，请检查文件下载路径（确保没有名为"savedrecs.txt"的文件）和文件保存路径（看看爬到哪条数据了），更换合适的起始点s，再次运行模块`4.自动化导出`，继续采集数据。
## 结语
本程序是我经过海量数据采集实践中用得比较习惯的最终版本，现分享给大家！<br>
欢迎各位同门提出新的方案或与我沟通交流，共同优化改进WOS文献数据的自动化采集程序！！！





