---
title: 01 restful 基本概念
date: 2019-12-23 18:14:10
tags:
  - restful
categories:
  - restful
topdeclare: true
reward: true
---

`REST` （representational state transfer） 架构风格是一种世界观，把信息提升为架构中的一等公民。通过 REST 可以实现系统的高性能、可伸缩、通用性、简单性、可修改性和可扩展等特性。
`REST` 即Representational State Transfer的缩写，可译为"表现层状态转化”。REST最大的几个特点为：资源、统一接口、URI和无状态。

<!--more-->

### 架构特点:
#### 资源  
  > 网络上的一个实体，或者说是网络上的一个具体信息。它可以是一段文本、一张图片、一首歌曲、一种服务，总之就是一个具体的实在。资源总要通过某种载体反应其内容，文本可以用txt格式表现，也可以用HTML格式、XML格式表现，甚至可以采用二进制格式；图片可以用JPG格式表现，也可以用PNG格式表现；JSON是现在最常用的资源表示格式。

- 资源是以json(或其他Representation)为载体的、面向用户的一组数据集，资源对信息的表达倾向于概念模型中的数据：
  - 资源总是以某种Representation为载体显示的，即序列化的信息
  - 常用的Representation是json(推荐)或者xml（不推荐）等
  - Representation 是REST架构的表现层

- 相对而言，数据（尤其是数据库）是一种更加抽象的、对计算机更高效和友好的数据表现形式，更多的存在于逻辑模型中.
  资源和数据关系如下：
  ![资源与数据](/zbcn.github.io/assets/postImg/restful/img/blog-post-rest-resource-vs-data.png)

#### 统一接口
> RESTful架构风格规定，数据的元操作，即CRUD(create, read, update和delete,即数据的增删查改)操作，分别对应于HTTP方法：GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源，这样就统一了数据操作的接口，仅通过HTTP方法，就可以完成对数据的所有增删查改工作。

即:
  - GET（SELECT）：从服务器取出资源（一项或多项）。
  - POST（CREATE）：在服务器新建一个资源。
  - PUT（UPDATE）：在服务器更新资源（客户端提供完整资源数据）。
  - PATCH（UPDATE）：在服务器更新资源（客户端提供需要修改的资源数据）。
  - DELETE（DELETE）：从服务器删除资源。

#### URI 统一资源定位符
> 可以用一个URI（统一资源定位符）指向资源，即每个URI都对应一个特定的资源。要获取这个资源，访问它的URI就可以，因此URI就成了每一个资源的地址或识别符。

#### 无状态

> 所谓无状态的，即所有的资源，都可以通过URI定位，而且这个定位与其他资源无关，也不会因为其他资源的变化而改变。

- 有状态

![有状态](/zbcn.github.io/assets/postImg/restful/img/有状态.jpg)

- 无状态

![无状态](/zbcn.github.io/assets/postImg/restful/img/无状态.jpg)

#### ROA、SOA、REST与RPC

- ROA即`Resource Oriented Architecture`，__RESTful 架构风格__ 的服务是围绕资源展开的，是典型的ROA架构（虽然“A”和“架构”存在重复，但说无妨），虽然ROA与SOA并不冲突，甚至把ROA看做SOA的一种也未尝不可，但由于RPC也是SOA，比较久远一点点论文、博客或图书也常把SOA与RPC混在一起讨论，因此，__RESTful 架构风格的服务通常被称之为ROA架构__ ，很少提及SOA架构，以便更加显式的与RPC区分。

- `RPC` 风格曾是Web Service的主流，最初是基于XML-RPC协议（一个 __远程过程__ 调用（ `remote procedure call`，RPC)的分布式计算协议），后来渐渐被 `SOAP`协议（__简单对象访问协议__（`Simple Object Access Protocol`））取代；RPC风格的服务，不仅可以用HTTP，还可以用TCP或其他通信协议。但RPC风格的服务，受开发服务采用语言的束缚比较大，如.NET框架中，开发web service的传统方式是使用WCF，基于WCF开发的服务即RPC风格的服务，使用该服务的客户端通常要用C#来实现，如果使用python或其他语言，很难实现可以直接与服务通信客户端；进入移动互联网时代后，RPC风格的服务很难在移动终端使用，而RESTful风格的服务，由于可以直接以json或xml为载体承载数据，以HTTP方法为统一接口完成数据操作，客户端的开发不依赖于服务实现的技术，移动终端也可以轻松使用服务，这也加剧了REST取代RPC成为web service的主导.

- RPC与RESTful的区别如下面两个图所示

![rpc风格](/zbcn.github.io/assets/postImg/restful/img/rpc风格.jpg)

![restful风格](/zbcn.github.io/assets/postImg/restful/img/restfull风格.jpg)

### 本真REST与hybrid风格
> 通常开发者做服务相关的客户端开发时，使用的所谓RESTful服务，基本可分为本真REST和hybrid风格两类。本真REST即我上文阐述的RESTful架构风格，具有上述的4个特点，是真正意义上的RESTful风格；而hybrid风格，只是借鉴了RESTful的一些优点，具有一部分RESTful的特点，但对外依然宣称是RESTful风格的服务。（窃以为，正是由于hybrid风格服务混淆了RESTful的概念，才在RESTful架构风格提出了本真REST的概念，以为了划分界限 :P）

> hybrid风格的最主流的用法是，使用GET方法获取资源，用POST方法实现资源的创建、修改和删除。hybrid风格之所以存在，据我了解有两种来源：一种情况是因为，某些开发者并没有真正理解何为RESTful架构风格，导致开发的服务貌合神离；而主流的原因是由于历史包袱 —— 服务本来是RPC风格的，由于上文提到的RPC的劣势及RESTful的优势，开发者在RPC风格的服务上又包装了一层RESTful的外壳，通常这层外壳只为获取资源服务，因此会按RESTful风格实现GET方法，如果客户端提出一些简单的创建、修改或删除数据的需求，则通过HTTP协议中最常用的POST方法实现相应功能。

> 开发RESTful 服务，如果没有历史包袱，不建议使用hybrid风格。

### 认证机制
![认证机制](/zbcn.github.io/assets/postImg/restful/img/认证机制.jpg)

由于RESTful风格的服务是无状态的，认证机制尤为重要。例如上文提到的员工工资，这应该是一个隐私资源，只有员工本人或其他少数有权限的人有资格看到，如果不通过权限认证机制对资源做一层限制，那么所有资源都以公开方式暴露出来，这是不合理的，也是很危险的。

认证机制解决的问题是，确定访问资源的用户是谁；权限机制解决的问题是，确定用户是否被许可使用、修改、删除或创建资源。权限机制通常与服务的业务逻辑绑定，因此权限机制需要在每个系统内部定制，而认证机制基本上是通用的，常用的认证机制包括 session auth(即通过用户名密码登录)，basic auth，token auth和OAuth，服务开发中常用的认证机制为后三者。

#### Basic Auth
> Basic Auth是配合RESTful API 使用的最简单的认证方式，只需提供用户名密码即可，但由于有把用户名密码暴露给第三方客户端的风险，在生产环境下被使用的越来越少。因此，在开发对外开放的RESTful API时，尽量避免采用Basic Auth

#### Token Auth
> Token Auth并不常用，它与Basic Auth的区别是，不将用户名和密码发送给服务器做用户认证，而是向服务器发送一个事先在服务器端生成的token来做认证。因此Token Auth要求服务器端要具备一套完整的Token创建和管理机制，该机制的实现会增加大量且非必须的服务器端开发工作，也不见得这套机制足够安全和通用，因此Token Auth用的并不多。

#### OAuth
> OAuth（开放授权）是一个开放的授权标准，允许用户让第三方应用访问该用户在某一web服务上存储的私密的资源（如照片，视频，联系人列表），而无需将用户名和密码提供给第三方应用。

> OAuth允许用户提供一个令牌，而不是用户名和密码来访问他们存放在特定服务提供者的数据。每一个令牌授权一个特定的第三方系统（例如，视频编辑网站)在特定的时段（例如，接下来的2小时内）内访问特定的资源（例如仅仅是某一相册中的视频）。这样，OAuth让用户可以授权第三方网站访问他们存储在另外服务提供者的某些特定信息，而非所有内容。

> 正是由于OAUTH的严谨性和安全性，现在OAUTH已成为RESTful架构风格中最常用的认证机制，和RESTful架构风格一起，成为企业级服务的标配。

> 目前OAuth已经从OAuth1.0发展到OAuth2.0，但这二者并非平滑过渡升级，OAuth2.0在保证安全性的前提下大大减少了客户端开发的复杂性，因此，Gevin建议在实战应用中采用OAuth2.0认证机制。

[原文](https://blog.igevin.info/posts/restful-api-get-started-to-write/)
