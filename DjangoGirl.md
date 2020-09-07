#### Django

0.1 相关资料
- 文档
    - 官方文档
- 教程
    - [简明教程666](https://python666.cn/static/djangogirl/djangogirl.html?page=2)
    - 菜鸟教程
- 书单
    - 京东    

---
###### Django 是什么

1.1 Django是什么
- Python编写的开源的Web框架

1.2 为什么需要一个框架
- 避免重复开发相似组件，无需重新造轮子，提高效率

1.3 当向Django服务器请求一个网站时，会发生什么？
- url解析器
- 视图函数

---
###### Django安装

2.1 虚拟环境
- 在Linux上创建虚拟环境 python3 -m venv myvenv
    - 其中myvenv是虚拟环境的名字
    - 上面的命令将创建一个名为 myvenv 目录 （或任何你选择的名字），其中包含我们的虚拟环境 （基本上是一堆的目录和文件）
2.2 使用虚拟环境        
- Linux运行进入虚拟环境 source myvenv/bin/activate
- 注意 （myvenv） 前缀的出现，提示表明已经进入 虚拟环境
2.3 在虚拟环境中安装Django
- 通过命令pip install django    

---
###### 第一个Django项目

3.1 创建一个新的Django项目

- 在虚拟环境中，运行命令 `django-admin startproject mysite .`
    - 作用：需要运行一些由 Django 提供的脚本，为我们即将开始的项目建立主要骨架。 它会生成一系列的文件夹和文件，在后面的项目中我们会需要修改和使用到它们。
    - 注意事项：记得不要漏掉命令后面的小点（.）；符号" . "很重要，它将告诉脚本程序自动安装Django到你当前选择的目录中
- 执行完命令后，会自动生成对应文件，目录结构如下
    - djangogirls
        - manage.py 一个帮助管理站点的脚本。在它的帮助下我们将能够在我们的计算机上启动一个 web 服务器，而无需安装任何东西。settings.py 文件包含的您的网站的配置数据。
        - mysite
            - setting.py 文件包含的您的网站的配置数据
            - urls.py 文件包含 urlresolver 所需的模型的列表。现在让我们忽略其他文件, 现在我们不会改变它们。要记住的唯一一点是不要不小心删除他们！
            - wshi.py
            - __ __init.__ __.py 初始化配置

3.2 更改配置

- 设定时区：在 settings.py文件中, 找到包含 TIME_ZONE 字段的这行，`TIME_ZONE = 'Asia/Shanghai'`
- 修改静态文件路径：在 settings.py文件中，下拉到文件的 最底部 , 就是在 STATIC_URL 条目的下面，添加新的内容 `STATIC_ROOT = os.path.join(BASE_DIR, 'static')`
    
3.3 设置数据库

- 默认使用sqlite3，在mysite/settings.py文件中应该默认已经有如下配置了

```
    DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

```    

- 创建数据库运行命令：`python manage.py migrate`
- 启动网络服务：
    - 进入包含 manage.py 文件的目录 （ djangogirls 目录下）。 在控制台中，我们可以通过运行 python manage.py runschmerver 开启 web 服务器
    - 通过浏览器访问`http://127.0.0.1:8000/`检测站点服务器是否已经在运行了
    - 停止服务 可以使用组合快捷键CTRL+C

---

###### Django 模型

4.1 背景知识——对象

- 面向对象编程
    - 属性——描述特征
    - 行为——操作方法

4.2 Django模型

- 存在与数据库中的一种特殊的对象

4.3 创建应用程序

- 为了让一切保持整洁，我们将我们的项目内部创建单独的应用程序，在虚拟环境中执行命令 `python manage.py startapp blog`
    - 一个新的 blog 目录被创建，它现在包含一些文件，目录结构如下
    - djangogirls
        - manage.py 一个帮助管理站点的脚本。在它的帮助下我们将能够在我们的计算机上启动一个 web 服务器，而无需安装任何东西。settings.py 文件包含的您的网站的配置数据。
        - mysite
            - __ __init.__ __.py 初始化配置
            - setting.py 文件包含的您的网站的配置数据
            - urls.py 文件包含 urlresolver 所需的模型的列表。现在让我们忽略其他文件, 现在我们不会改变它们。要记住的唯一一点是不要不小心删除他们！
            - wsgi.py
        - blog
            - migrations
                - __init.__ __.py
            - __ __init.__ __.py
            - admin.py
            - models.py
            - tests.py
            - views.py    

- 关联到Django项目中
    - 在 mysite/settings.py 文件中这样做的。 我们需要找到 INSTALLED_APPS 并在它下面添加一行 'blog'

4.4 创建博客文章模型

- 在 blog/models.py 文件中，定义所有的 Models 对象— — 我们将在其中都定义我们的博客文章。

4.5 在数据库中为模型创建数据表

- 将我们新的模型添加到我们的数据库。 首先我们必须让Django知道我们在我们的模型(我们刚刚创建的！) 有一些变更。 输入 `python manage.py makemigrations blog `
- Django为我们准备了我们必须应用到我们数据库的迁移文件。输入 `python manage.py migrate blog`


###### Django admin 管理后台
本节目标：通过Django admin 来添加，编辑和删除文章

5.1 注册Post模型

- 打开blog/admin.py文件，并替换其中的文件内容，下列


		form django.contrib import admin
		form .models import Post

		admin.site.register(Post)

	

- 上面的操作导入了4part中定义的Post模型，通过admin.site.register(Post)来注册模型。目的为了让我们的对象模型可见

5.2 登陆后台查看Post模型

1. 首先启动服务器，通过浏览器进入后台登陆页面
    - 控制台输入 python manage.py runschmerver 启动服务器
    - 打开浏览器，输入地址 http://127.0.0.1:8000/admin/ 
2. 注册管理员账户
    - 命令行，输入 python manage.py createsuperuser ，按下Enter
    - 再输入你的用户名(英文小写，不包括空格), 邮箱和密码 ，按下Enter    
        - 输入密码是不显示（这是正常的）
3. 返回浏览器，用刚才注册的超级用户来登录，然后应该能看到Django admin的管理面板
4. 尝试到Post页面发布一些文章

###### 部署

本节目标：在互联网上发布你的应用程序的一系列过程，因此人们最终可以一起去看看你的应用程序；

- 服务器供应商：通过[pythonanywhere](https://www.pythonanywhere.com/)
    - 是什么
        - 类似的免费平台还有 Heroku，Openshift 等，收费平台有阿里云、亚马逊 AWS、微软 Azure 等
    - [怎么用](https://zhuanlan.zhihu.com/p/24650061)
        1. 新建项目
        2. 部署已有的项目
- [git](http://rogerdudler.github.io/git-guide/index.zh.html)
    - 如何初始化本地仓库
    - 常用git命令管理版本
    - 本地与githua服务关联
- 配置pythonanywhere

6.1 安装并设置pythonanywhere

- 首先，让我们在PythonAnywhere（ www.pythonanywhere.com ）注册（ https://www.pythonanywhere.com/pricing/ ）一个“Beginner”账户。
    - 注意 在这里选择的用户名会出现在博客链接的地址当中 yourusername.pythonanywhere.com ，因此最好选择你自己的绰号或者是与博客内容相关的名字。
- 设置 ALLOWED_HOSTS值
    - ALLOWED_HOSTS 是为了限定请求中的host值，以防止黑客构造包来发送请求，保证只有在列表中的host才能访问
    - 打开你的 djangogirl 项目，进入 mysite/settings.py，找到里面的 ALLOWED_HOSTS ，未设置前应该是这样：`ALLOWED_HOSTS = []`        
    - 现在，将你在 PythonAnywhere 的地址和本地地址加入 ALLOWED_HOSTS ，加入后应该是这样:`ALLOWED_HOSTS = ['yourusername.pythonanywhere.com', '127.0.0.1']`
        - 注意 ALLOWED_HOSTS 里面的 yourusername 应该换成你自己的。

6.2 安装并设置git

- git初始化django代码
    - 打开你的终端，进入 djangogirls 文件夹运行以下的命令： 
    ```
    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    ```
- 配置忽略文件
    - 在系统根目录下创建一个命名为 .gitignore 的文件。 打开编辑器，创建新文件并写入以下内容,并保存
    ```
    *.pyc
    __pycache__
    myvenv
    db.sqlite3
    .DS_Store
    ```    
- 使用git来跟踪代码，常用的命令有
    - git add 添加待跟踪的文件    
    - git status 查看文件的状态
    - git commit 提交文件状态
- 推送到github上
    - 注册/登陆自己的github账号
    - 创建新的代码仓库，获取对应的URL地址
    - 把本地的Git仓库和GitHub上的挂接
6.3 在Pythonanywhere上拉取上传的代码       

1. 当然注册完 PythonAnywhere，你讲会转到仪表盘或“控制台”页面。 选择启动“Bash”控制台这一选项 — 这是 PythonAnywhere 版的控制台，就像你本地电脑上的一样。
        - 注意 PythonAnywhere 基于 Linux，因此如果你使用 Windows，控制台将会和你本地电脑上的略有不同。
    - 让我们通过创建一个我们仓库的 “Clone” 以便从 GitHub 拉取代码到 PythonAnywhere。 在 PythonAnywhere 控制台输入以下 (不要忘记使用 GitHub 用户名替换 <your-github-username> )：
        `git clone https://github.com/<your-github-username>/my-first-blog.git`
        - 这将会拉取一份你的代码副本到 PythonAnywhere 上。通过键入 tree my-first-blog 查阅

2. 在 PythonAnywhere 上创建 virtualenv
    - 如同你在自己电脑上做的，你可以在 PythonAnywhere 上创建 virtualenv 虚拟环境。在 Bash 控制台下，键入（请把 python3.6 换成你在本地使用的 python 版本）
    - 前方有坑出没，请注意 pip 安装 步骤可能需要几分钟。 耐心，耐心！但是如果超过 5 分钟，就不对劲了。

```
$ cd my-first-blog

$ virtualenv --python=python3.6 myvenv
Running virtualenv with interpreter /usr/bin/python3.6
[...]
Installing setuptools, pip...done.

$ source myvenv/bin/activate

(mvenv) $  pip install django
Collecting django
[...]
Installing collected packages: pytz, sqlparse, django
Successfully installed django-2.2.6 pytz-2019.3 sqlparse-0.3.0
```                 

3. 收集静态文件
    - 静态文件是很少改动或者并非可运行的程序代码的那些文件，比如 HTML 或 CSS 文件。 在我们的计算机上，它们以不同的方式工作。
    - 暂且我们只需要在服务器上运行一个额外的命令，就是 collectstatic 。 它告诉 Django 去收集服务器上所有需要的静态文件。 就眼下来说主要是使admin管理界面看起来更漂亮的文件。
次命令执行两边`(mvenv) $ python manage.py collectstatic`，再输入yes

4. 在Pythonanywhere上创建数据库
    - 注意：服务器与你自己的计算机不同的另外一点是：它使用不同的数据库。因此用户账户以及文章和你电脑上的可能会有不同。
    - 像在自己的计算机上一样在服务器上初始化数据库，使用 migrate 以及 createsuperuser ：

```
(mvenv) $ python manage.py migrate
Operations to perform:
[...]
  Applying sessions.0001_initial... OK


(mvenv) $ python manage.py createsuperuser

Username: your name
Email address:
Password:
Password (again):
Superuser created successfully.
```        

5. 将博客发布为网络应用程序
- 发布之前的确定：当前我们的代码已在PythonAnywhere上，我们的 virtualenv 已经准备好，静态文件已收集，数据库已初始化。
- 步骤
    1. 通过点击页面左上角的 蟒蛇 logo 返回到 PythonAnywhere 仪表盘，然后点击 Web 选项卡。最终，点 Add a new web app .
    2. 在确认你的域名之后，选择对话框中 manual configuration (注 不是 "Django" 选项) ： 下一步选择 Python 3.6（这里请与虚拟环境的 python 版本一致，虚拟环境只能是 python 3.5 - 3.7） ，然后点击 Next 以完成该向导。
        - 注意 确保你选中 "Manual configuration" 选项，而不是 "Django" 那个。我们太牛逼，所以不要用 PythonAnywhere Django 默认设置 ;-)
    3. 设置 virtualenv：你将会被带到 PythonAnywhere 上你的Web 应用程序的配置屏，那个页面是每次你想修改服务器上你的应用程序时候要去的页面。在 “Virtualenv” 一节，点击红色文字 “Enter the path to a virtualenv"，然后键入： /home/<your-username>/my-first-blog/myvenv/ 。 前进之前，先点击有复选框的蓝色框以保存路径。
        - 注意 替换你自己的用户名。如果你犯了错，PythonAnywhere 会显示一个小警告。
    4. 配置 WSGI 文件：Django 使用 “WSGI 协议”，它是用来服务 Python 网站的一个标准。PythonAnywhere 支持这个标准。 PythonAnywhere 识别我们 Django 博客的方式是通过配置 WSGI 配置文件。    
        - 点击 “WSGI configuration file” 链接（在 "Code" 一节，接近页面上方 — 它将被命名为如 /var/www/<your-username>_pythonanywhere_com_wsgi.py ），然后跳转到一个编辑器。删除所有的内容并用
        以下内容替换
        - 这个文件的作用是告诉 PythonAnywhere 我们的Web应用程序在什么位置，Django 设置文件的名字是什么。完成后点击 Save 然后返回到 Web 选项卡
        - 注意 当看到 <your-username> 时，别忘了替换为你自己的用户名。
    5. 配置静态文件地址
        - 存取问题：你的网站已经成功部署在 PythonAnywhere 上了，但目前还有一个小问题，就是当你访问 http://<your-username>.pythonanywhere.com/admin/（Django 后台 admin 页面）的时候，会发现 admin 页面还没有任何样式
        - 因为静态文件还没有被成功加载，我们需要配置下静态文件的路径，让我们能通过 url 访问到我们已经收集在 static/ 文件夹中的静态文件。静态文件在 PythonAnywhere Web 选项卡的 Static files 节中进行配置
        - 其中，URL 我们统一使用 /static/ 以方便后面的操作，Directory 中是你静态文件在项目中的位置，这里我们使用完整路径：/home/<your-username>/my-first-blog/static/。
            - 注意 你要将 Directory 的路径改成你自己的静态文件路径，如果你之前完全按照我们的教程进行操作，你只用将 <your-username> 替换为你自己的用户名。
        - 这样，我们就可以通过网址 http://<your-username>.pythonanywhere.com/static/子文件夹1/文件1 来访问静态文件夹 /home/<your-username>/my-first-blog/static/ 中 子文件夹1 中的 文件1。
        - 配置完以后，点击 Web 页面最上方大大的绿色 Reload 按钮。访问一下 http://<your-username>.pythonanywhere.com/admin/，就可以看到成功加载了静态文件    
```
# WSGI configuration file 编辑内容

import os
import sys

path = '/home/<your-username>/my-first-blog'  # use your own username here
if path not in sys.path:
    sys.path.append(path)

os.environ['DJANGO_SETTINGS_MODULE'] = 'mysite.settings'

from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()
```        

6.4 Tips: 
如果你在访问你的网站时候看到一个错误，首先要去 error log 中找一些调试信息。 你可以在 PythonAnywhere Web 选项卡 中发现它的链接。 检查那里是否有任何错误信息，底部是最新的信息。 常见问题包括：

- 忘记我们在控制台中的步骤之一：创建 virtualenv，激活它，安装 Django 进去，运行 collectstatic，migrate 迁移数据库。
- 在 Web 选项卡中，virtualenv 路径设置错误 — 如果真是这样，这通常会是一个红色错误消息
- WSGI 文件设置错误 — 你的 my-first-blog 目录地址设置是否正确？
- 你是否为你的 virtualenv 选择了同样的 Python 版本，如同 Web 应用程序里的那样？两个应该都是 3.6。
- 有一些常见的调试小贴士在 general debugging tips on the PythonAnywhere wiki 里.

6.5 最后验证一下：

你网站的默认页面说 “Welcome to Django”，如同你本地计算机上的一样。 试着添加 /admin/ 到URL的末尾，然后你会到达管理者的页面。 输入用户名和密码登录，然后你会看到服务器上的 add new Posts 。    
