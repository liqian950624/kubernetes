#### 部署一个server
-   弄清所要部署server的功能：只有详细了解所部署server的功能，才能设计该server框架。如：
    -   部署一个nginx-PHP
    ```
    功能详解：该server包含三个部分；第一部分：一个web界面，用户通过该web界面发出一个写操作请求；第二部分：接受用户发出的请求，将请求写入到本地某一文件内，并将
    请求转发到第三部分；第三部分：接收请求，并将请求写入数据库中。然后使用日志收集工具收集各个部分日志，统一存储。
    完成第二部分后，将用户请求
    ```
-   根据该server的功能，设计部署架构（尽量解耦）。如：
    -   设计架构（部分介绍）
    ```
    根据server功能可分为两大部分：一部分接收并相应请求，另一部分收集日志。根据第一部分功能需求可设计nginx+php：nginx作为代理服务器，
    使用php实现具体操作，如：设计好用户界面，当用户访问界面一（上一步骤的第一部分）时，写入请求内容，然后post到另一界面（上一步骤的第二部分）；
    ```
##### 注：最好将前两部在具体实施之前做一份文档，该文档至少包含：server功能、架构设计、架构详解。
-   根据设计的好架构，安排合理的工作计划。此部分为重要部分。
    -   一般根据server功能做计划。如：
    ```
    以步骤一实例为例：因为要以web形式用户使用，所以需选择nginx或apache其一来显示页面；根据server功能需要设计前台页面和后台处理程序，所以需要编写HTML+php；
    以此，整体计划可是设计为：编写用户请求页面 - 编写接收并响应写入本地文件PHP - 编写接收并响应写入数据库 - 收集日志。
    ```
    -   解耦化安排
    ```
    所部署的服务尽量解耦。解耦可方便调试，同时具有微服务的思想。
    ```
-   具体实施：一般包含三大步：本地测试，部署测试、最终部署
    -   本地测试
        -   镜像选择：大部分镜像可在docker hub中查找（首选官网镜像）。若网上的镜像无法满足需求，需手动创建镜像。
        -   对一些没用过或复杂的软件，在使用容器部署前可先本地安装再使用容器部署。
    -   部署测试，使用kubernetes部署首先编写yaml或json文件，然后部署测试该文件是否满足需求。
    -   最终部署：根据调试好的部署文档实施最终部署。
    
   