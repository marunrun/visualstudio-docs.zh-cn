---
title: Visual Studio Shell （集成） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, integrated mode features
- Shell [Visual Studio], integrated mode features
ms.assetid: 0b40d495-f17f-4bb9-ace8-b365a7172784
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4f6e88e5c430129faa80f34a45f9b6620d5b0d13
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850364"
---
# <a name="visual-studio-shell-integrated"></a>Visual Studio Shell（集成）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 集成 Shell 包括集成开发环境 (IDE)、调试程序以及源控件集成。 不包含任何编程语言。 但是，集成 shell 提供了一个框架，可用于添加编程语言。  
  
 Visual Studio 集成 shell 实际上是 Visual Studio 独立 shell 的组合，另外还有一个包含集成的 shell 特定组件的其他安装。  集成 shell 应用程序应同时包含[Microsoft Visual Studio Shell (独立) 可再发行组件包](https://docs.microsoft.com/collaborate/connect-redirect?ProgramID=8963&InvitationID=VS15-2R69-RB8J)中的独立 shell 可再发行组件包，以及[Microsoft Visual Studio Shell (集成) 可再](https://docs.microsoft.com/collaborate/connect-redirect?ProgramID=8963&InvitationID=VS15-2R69-RB8J)发行组件包中的集成 shell 可再发行组件包。  
  
> [!NOTE]
> 您必须先填写一份简短的客户调查，然后才能获取独立和集成 Shell 可再发行组件包。  填写完客户调查后，您会转到包含可再发行组件包下载链接的 Visual Studio Connect 页面。  可以在后续访问 visual studio **2015 集成和隔离 SHELL &#124;** 选项卡下的 visual studio Connect 站点时找到下载链接。  
  
 如果在与 Visual Studio 完整版本相同的计算机上安装集成 shell 应用程序，则应用程序的组件将直接集成到 Visual Studio 中。  
  
## <a name="features-in-the-integrated-shell"></a>集成外壳中的功能  
  
|||  
|-|-|  
|功能区域|功能|  
|语言支持|-无|  
|IDE|<ul><li>设置<br /><br /> <ul><li>创建设置</li><li>导入和导出设置</li><li>重置设置</li></ul></li><li>**工具箱**集成</li><li>**任务列表**集成</li><li>帮助集成</li><li>"**选项**" 对话框</li><li>字体和颜色管理</li><li>**输出**窗口</li><li>**命令**窗口</li><li>窗口管理</li><li>命令、菜单和键绑定</li><li>域特定语言（DSL）运行时</li></ul>|  
|项目系统和项目类型|-解决方案和解决方案文件夹<br />-解决方案配置管理器<br />-项管理<br />-单项目和多项目解决方案<br />-应用程序设计器（简化项目属性）<br />-添加 Web 引用<br />-添加服务引用<br />-单项目<br />-网站项目类型<br />-Web 应用程序项目|  
|生成|-IDE 中的自定义生成步骤<br />-知识产权预编译（IP）保护<br />-代码签名<br />     MSBuild|  
|编辑器|-代码浏览工具（统一查找、源定义、继承）<br />-代码导航<br />-IntelliSense<br />-   SmartTags<br />-重构<br />-整齐列表<br />-IntelliSense 筛选<br />-   **代码定义**"窗口|  
|Designer|-Windows Presentation Foundation 设计器<br />-Windows 窗体设计器<br />-Web 设计器和 HTML 编辑器|  
|数据|-   **服务器资源管理器**（简体：仅限数据）。 请参阅备注 1。<br />"-   **数据源**" 窗口<br />-完整的数据控件集<br />-XML 编辑器<br />-数据绑定到本地数据源（.MDF 或.MDB<br />-数据绑定到对象<br />-到 Web 服务的数据绑定<br />-数据绑定到本地数据库服务器<br />-数据绑定到远程数据库服务器<br />-用于远程数据的 DDL 工具<br />-   **服务器资源管理器**扩展性（[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 示例）|  
|调试器|-本地调试。 请参阅注释2。<br />-托管调试<br />-本地调试<br />-附加到本地进程<br />-附加到远程进程<br />-匿名委托<br />-应用程序域<br />-ASPX 调试<br />-特性<br />在 Func-eval 期间中断<br />-断点<br />-断点约束<br />-调用堆栈<br />-   **命令**窗口<br />-跨线程调试<br />-数据提示<br />-数据可视化工具<br />-对托管调试助手（Mda）的调试器支持<br />-为类型转发器提供调试器支持<br />-DTEEvents 对 OTB 的支持<br />-JMC 分档器<br />-调试器 AppID 测试（DBGCLR）<br />-调试器配置文件<br />-调试器工具和选项<br />-调试迭代器<br />-设计时表达式计算<br />- C#表达式计算器<br />-反汇编<br />-编辑并继续<br />-表达式计算器窗口（监视、局部变量、自动）<br />-异常帮助程序<br />-异常<br />-执行<br />-   泛型<br />-获取正确的源<br />-HPC/群集调试<br />-集成多语言调试<br />-互操作调试<br />-实时调试<br />-本地调试<br />-托管调试<br />-手动控制（"进程" 窗口）<br />-   内存<br />-小型转储支持<br />-模块<br />-多进程调试<br />-本机调试<br />-新的调试引擎支持<br />-优化代码调试<br />-输出 windows 筛选<br />-托管调试的进程托管<br />-进程<br />-快速监视<br />-寄存器<br />-在堆栈中注册<br />-远程调试<br />-返回值<br />-脚本调试<br />-源服务支持<br />-安全性<br />-并排<br />-   SQL<br />-符号服务器<br />-跟踪点<br />-Thread<br />-可视化<br />-可扩展样式表语言转换（XSLT）调试器|  
|64 位支持|-64 适用于托管和本机代码的位调试，所有语言<br />-x64 本机支持|  
|源代码管理（SCC）|-基本 SCC 集成。 请参阅备注 3。<br />-工具和选项验证|  
|可扩展性|-使用 Vspackage 和 MEF 组件|  
  
## <a name="notes"></a>注释  
  
#### <a name="1-data-tools"></a>1. 数据工具  
 集成外壳包含数据库开发工具，如数据扩展性支持和简化的**解决方案资源管理器**。 不过，不会将 SQL Server Express、SQL Reporting 和 Crystal 报表包含在集成 shell 中。  
  
#### <a name="2-debugging-support"></a>2. 调试支持  
 集成外壳包含在 Visual Studio 的社区版本中包含的相同调试引擎。 调试引擎包括适用于托管代码的常见调试器，还包括相关功能，如 "运行"、"附加"、"设置断点"、"编辑并继续" 等。 不过，调试引擎不支持 SQL Server 数据库调试。  
  
 尽管基本调试器包中包含对本机调试的支持，但无法对其进行扩展以支持其他语言。  
  
#### <a name="3-source-code-control-integration"></a>3. 源代码管理集成  
 集成 shell 提供用于实现源代码管理（SCC）的 Api，并提供基于 MSSCCI 的公共源代码管理集成组件。  
  
 尽管 SCC 集成并非 Visual Studio Pro 版本的常规功能，但集成外壳中提供了 SCC 集成。  
  
#### <a name="4-build-support"></a>4. 生成支持  
 集成 shell 提供生成支持。 可以在[MSBuild 引用](../msbuild/msbuild-reference.md)中找到有关生成的信息。  
  
## <a name="features-not-included-in-the-integrated-shell"></a>未包括在集成 Shell 中的功能  
 下面列出了未包含在集成 shell 中的功能：  
  
- 类设计器  
  
- PreEmptive Protection - Dotfuscator  
  
- 语言功能  
  
- VSHost  
  
- 集成外壳中不包含 Visual Studio 语言或其关联的项目模板或项目项模板。 不包含其他功能的特定于语言的实现，例如 Visual Basic 代码片段。  
  
## <a name="see-also"></a>请参阅  
 [扩展 Visual Studio 概述](https://msdn.microsoft.com/library/3e9078d7-2763-4cc4-8e20-fac69d747f59)
