# Python
Django
1. Django框架介绍
    1. 什么是Django
        Django是一个开源框架,采用Python语言编写的
        早期时主要做新闻和内容管理的网站
        Django 本身提供了非常强大的后台管理系统
2. Django框架的使用
    1. 创建项目
        1. 创建目录
            作用: 用于保存所有的Django项目(可选)
            指令: mkdir django
        2. 创建项目
            cd django
            使用 django-admin 指令创建 Django 项目
            语法 : django-admin startproject
    2. Django项目的结构介绍
        1. manage.py
            包含执行django中的各项操作的指令(子命令)
            如:
                启动服务: runserver
                创建应用: startapp
                创建管理员: createsuperuser
        2. 主目录 (主文件夹, 与项目名称一致的目录)
            1. __init__.py
                项目的初始化文件,服务被启动,该文件自动被运行
            2. urls.py
                项目的基础url配置文件(基础的路由配置)
            3. wsgi.py
                Web Server Gateway Interface
                Web服务网关接口
            4. settings.py
                项目的配置文件
                1. BASE_DIR : 获取当前项目的绝对路径
                2. DEBUG : 是否启用调试模式
                    True : 启用调试模式 (开发坏境中推荐)
                    False : 不启用调试模式 (生产坏境中推荐)
                3. ALLOWED_HOSTS 
                    设置允许访问到本项目的地址列表
                    如果为空的话,只有本机(localhost/127.0.0.1)才能访问

                    如果允许在局域网中被外部机器访问的话:
                    推荐写 ['*'], 表示任何能够表示该机器的地址都能访问到当前项目
                    
                    如果允许被其它机器访问的话, 启动服务时,必须使用以下方式:
                        ./manage.py runserver 0.0.0.0:端口号
                4. INSTALLED_APPS
                    指定已安装的应用,如果有自定义应用的话,需要在此注册
                5. MINDDLEWARE
                    中间件, 如果有自定义的中间件, 需要在此注册
                    每一个中间件都可以拦截请求和响应
                6. ROOT_URLCONF
                    用于指定项目的基础路由配置文件
                7. TEMPLATES
                    指定模板的信息
                8. DATABASES
                    指定数据库的信息
                9. LANGUAGE_CODE
                    语言设置, 如果需要中文的话, 允许将值更改为 "zh-Hans"
                10. TIME_ZONE
                    指定时区, 中国时区的话, 允许将值设置为"Asia/Shanghai"
        3. 通过 url向视图传参
            1. 使用正则表达式进行传参
                使用子组传参,一个子组就是一个参数,要传递多个参数的话需要使用多个子组, 中间用 / 隔开
                子组 - () 
                urlpattern = [
                    # 当访问路径是show/的时候, 交给show_views 处理
                    url(r'^show/$',show_views),
                    # 当访问路径是show/两位数字的时候, 交给show1_views处理
                    url(r'^show/(\d{2})/$',show1_views),
                    # 两位字符  (\w{2})
                ]

                views.py
                def show1_views(request,num1):
                    num1 表示的就是路径 "show/" 后面的第一个参数
                    pass
                
            2. 使用url() 第三个参数 - 字典传参
                dic = {
                    'name' : "naruto",
                    'age' : 18 ,
                }

                url(r'^show3/$',show3_views,dic)

                views.py:
                def show3_views(request,name,age):
                    pass
