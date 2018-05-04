### 下载项目

```
git clone https://git.oschina.net/vakinge/jeesuite-bestpl.git
```

### 编译项目

```
mvn clean package -DskipTests=true
```

**最终生成部署包为：**

* dubbo服务:bestpl-dubbo/target/bestpl-dubbo-dist.zip
* springboot web：bestpl-springboot/target/bestpl-springboot.jar
* rest API:bestpl-rest/target/bestpl-rest.war

### 项目部署

**说明**：

* 目前没有前后端分离所以rest API模块暂时用不上，无需部署。
* 以下演示`基础环境`\(mysql、kafka、redis、zookeeper\)和`配置中心`部署在阿里云
* 如果需要使用本地基础环境，请修改每个模块配置项`jeesuite.configcenter.profile`为`local`

  > redis：端口:6379，密码：123456
  >
  > mysql：database:bestpl\_db ，用户名：root，密码：123456 ，脚本：doc/table.sql
  >
  > kafka：端口：9092
  >
  > zookeeper：端口：2181

* 如果需要本地搭建配置中心参考：[部署配置中心](./confcenter.md)

---

* 步骤一：分别将以上构建的部署包拷贝到部署目录，如：/datas/deploy目录下。
* 步骤二：部署dubbo服务
  ![](http://ojmezn0eq.bkt.clouddn.com/duubo-deploy-1.png)启动成功，如下：

```
2017-09-17 11:22:13.752 INFO [main][AppServer.java:31] - 启动app-server....
==============================
|---------服务启动成功----------|
==============================
```

* 步骤三：部署springboot
  ```
  nohup java -jar bestpl-springboot.jar > bestpl-springboot.out 2>&1 &
  ```

启动成功后，访问：[http://127.0.0.1:8081/](http://127.0.0.1:8081/)  查看效果

#### 首页效果

![image](http://ojmezn0eq.bkt.clouddn.com/bestpl_snapshot.png)

---

### 基于docker发布

```
#切换到项目目录
cd /你的项目目录/jeesuite-bestpl
#打包，发布镜像到docker（下载镜像可能耗时很久）
mvn clean install -DskipTests=true -Pdocker
#启动
docker-compose up -d
```

---

### eclipse调试运行

1. **dubbo**：运行`AppServer.java`
2. **rest**:通过`mvn jetty:run`运行
3. **springboot**：运行`Application.java` 


