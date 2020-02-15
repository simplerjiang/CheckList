# CheckList
（开发中）全平台检查单 (Developing) All platform Checklist services

---

## 设计理念 Design concept

在很多场景下，我们时常需要面对一些重要必不可缺却又固定的操作或检查。例如项目上线，应用部署，当然这不仅仅适用于软件开发维护测试等场景中，即便在非计算机领域依然能起到重要的作用。


On different sences, we have to face some important and indispensable operational or testing. Example as project publish, application depoly, but it not only suitable on software development cases, also available to others fields.

为了解决复用，存储，跨平台，分享等功能，同时也为了提高效率，便有了创建一个全平台检查单应用，借助于.Net 与.Net Core技术。它将会包括网页端，桌面端，移动端。项目旨在作为一个全栈练手项目，当然即便在很忙的情况下，依然希望未来真的能开发并迭代几个版本（毕竟事情真的太多且想法也太多）

To deal with reuse, data storage, all platform, share this features, I got a idea to make a all platform depending on .Net and .Net Core framework. It will include Website, Desktop, Mobile. The project was defined as a full stack toy project, but I really hope that I have enough time and ability to finish it.

由于项目设想相对有些庞大，我也愿意接受任何希望参与开发的开发者，当然可能并不是以PR的方式进行参与，而是作为一个真正代码参与者，以保证项目能按照核心思想，方向，代码规范正常进行。当然也欢迎任何PR，我会认真阅读并考虑是否合并。

Becase of the project got a huge plan, I accept any who want to join the development developers. The work will not develop as Pull Request way, but work as a team work, to protect project follow the right core ideas, path, specification. Otherwhile, it still accept Pull Request, it will be merge after check and test.

---

## 技术方向

### 后端

应采用**asp.net core 2.2**, 我认为这是目前较为成熟稳定且拥有足够经验，库，替代方案的框架版本。 或采用WebApi + JWT（或Cookie双验证），至于是否包含CRUD未定。它将提供所有的接口及数据管理。

后端获或将采用开放式接口，即对**一切客户端开放**，这说明任何开发者都可以开发自己的客户端，并接入系统。为了保持向前兼容，接口设计将百分百遵循**开闭原则**，即永远不对旧版接口进行版本更新。


### 网页端

或采用Blazor Server， 考虑到后期迭代及重构的可能，本着就要尝鲜的精神，原本希望能直接上Blazor WebAssmebly, 但是经过一番实验发现其在3.1的预览版中的表现，并不能适用于生产环境。当然谁也不能保证，当真正写到网页端时,Blazor WebAssmebly已经出了呢。

### 移动端

应采用Xamarin， 作为忠诚的.Neter，个人觉得相较于原生开发，Xamarin效率更高，且更舒服，且本身应用功能较为简单，所以决定采用。

### 桌面端

毋庸置疑的WPF，这里就不过多解释，除非当真开始写的时候微软已出下一代惊人技术。

### 跨平台控制台应用？

额，用处不大，未定。

---

## 主要模型

#### 检查单模版（CheckListTemplate)

创建检查单模版，当真正使用检查单时，将自动复制成一个**检查单(CheckListEntity)**。
同时检查单模版具备分享，被全站查询，分裂复制（fork）等功能，达到多人复用的功能。

```c#
public class CheckListTemplate
{
  //主键
  [Key]
  public GUID ID {get;set;}
  
  //检查单个体模版
  public List<CheckListItemTemplate> Items {get;set;}
  
  //创建时间
  public DateTime CreateTime {get;set;}
  
  //是否来自fork
  public bool IsFork {get;set;}
  
  //如果是fork，原作者ID
  public string OrignOwnerID {get;set;}
  
  //被使用的次数
  public long UsedTimes {get;set;}
  
  //修改日志
  public List<TemplateChangeLog> Logs {get;set;}
  
  //拥有者
  public User Owner {get;set;}
  
  //检查单们
  public List<CheckListEntity> Entitys {get;set;}
  
  //是否允许（用于软删除）
  public bool IsEnable {get;set;}
  
}
```


#### 检查单个体模版(CheckListItemTemplate)

检查单中每一项检查的类，即存储顺序，标题，详细内容，附加文件


```c#
public class CheckListItemTemplate
{
  //主键
  [Key]
  public GUID ID {get;set;}
  
  //标题
  public string Title {get;set;}
  
  //详细内容
  public string Detail {get;set;}
  
  //附加文件
  public List<ItemFile> Files {get;set;}
  
  //创建实际
  public CreateTime 
}
```



