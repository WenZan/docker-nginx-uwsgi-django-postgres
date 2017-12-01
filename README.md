网站服务部署说明
---

该网站服务利用docker容器技术进行搭建，方便部署与迁移。

### 网站服务整体结构
```
Nginx + uwsgi + django + postgreSQL
```
<br>
由三个微服务组成，每个微服务使用一个容器：

* `Nginx服务` ： 容器名为nginx，安装了Nginx，nginx服务器监听django-uwsgi的8001端口；开放80端口，与宿主机80端口绑定
* `app服务` : 容器名为django-uwsgi，安装了uWSGI与Django，uWSGI服务器监听django-uwsgi的8001端口
* `db服务` : 容器名为db，安装了PostgreSQL，开放5432端口
* `adminer服务`： 容器名为adminer，额外的一个服务，用来查看数据库信息。开放8080端口。查看postgreSQL数据库可以访问http://localhost:8080网址，选择PostgreSQL，Server=db，User=postgres，Password=password。


### 部署要点
#### `code`目录用来存放网站应用程序以及各配置文件
* 子目录`django-uwsgi`用来存放django应用程序`app`以及django-uwsgi容器相关配置文件，其中requirements.txt文件用来包含django应用程序所需python库文件
* 子目录`nginx`用来存放nginx容器的相关配置文件
<br>

部署时按需求可能要更改code目录下各配置文件。若各配置已按需更改，即可在`docker-compose.yml`文件所在目录运行`docker-compose up`命令开启网站服务。

