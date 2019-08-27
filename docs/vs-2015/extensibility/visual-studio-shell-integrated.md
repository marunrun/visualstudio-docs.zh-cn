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
ms.openlocfilehash: 664363740737eb72213b4818b104aa14c3667a14
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65690932"
---
# <a name="visual-studio-shell-integrated"></a>Visual Studio Shell （集成）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 集成 shell 包括集成的开发环境 (IDE)、 调试器和源代码管理集成。 包含任何编程语言不。 但是，集成的 shell 提供一个框架，允许您添加的编程语言。  
  
 Visual Studio 集成 shell 是实际的 Visual Studio 独立 shell 与其他安装，其中包括集成的 shell 特定组件的组合。  集成的外壳应用程序应包括这两个独立的 shell 可再发行组件包从[Microsoft Visual Studio Shell （独立） Redistributable Package](http://go.microsoft.com/fwlink/?LinkId=616022)以及集成的 shell 可再发行组件包从[Microsoft Visual Studio Shell （集成） Redistributable Package](http://go.microsoft.com/fwlink/?LinkId=616021)。  
  
> [!NOTE]
> 在可以访问独立和集成 shell 可再发行组件包之前，系统将要求填写份简短的客户调查。  填写调查之后, 你将定向到 Visual Studio Connect 页面使用可再发行组件包下载链接。  可以在以后访问下的 Visual Studio Connect 站点上找到的下载链接**程序&#124;VISUAL STUDIO 2015 集成和独立 SHELL**选项卡。  
  
 如果在作为完整版本的 Visual Studio 在同一台计算机上安装集成的外壳应用程序，将在 Visual Studio 中直接集成应用程序的组件。  
  
## <a name="features-in-the-integrated-shell"></a>集成外壳中的功能  
  
|||  
|-|-|  
|功能区域|功能|  
|语言支持|-None|  
|IDE|<ul><li>设置<br /><br /> <ul><li>创建设置</li><li>导入和导出设置</li><li>重置设置</li></ul></li><li>**工具箱**集成</li><li>**任务列表**集成</li><li>帮助集成</li><li>**选项**对话框</li><li>字体和颜色管理</li><li>**输出**窗口</li><li>**命令**窗口</li><li>窗口管理</li><li>命令、 菜单和键绑定</li><li>域特定语言 (DSL) 运行时</li></ul>|  
|项目系统和项目类型|-解决方案和解决方案文件夹<br />-解决方案配置管理器<br />项目管理<br />-单项目和多项目解决方案<br />-应用程序设计器 （简化的项目属性）<br />-添加 Web 引用<br />-添加服务引用<br />-单项目<br />Web 站点项目类型<br />-Web 应用程序项目|  
|Build|的在 IDE 中自定义生成步骤<br />-预编译的知识产权 (IP) 保护<br />代码签名<br />     MSBuild|  
|编辑器|-代码浏览工具 （统一的查找、 源定义，继承）<br />代码导航<br />-   IntelliSense<br />-   SmartTags<br />-重构<br />-整齐排列<br />-IntelliSense 筛选<br />-   **代码定义**窗口|  
|Designer|-Windows Presentation Foundation 设计器<br />-Windows 窗体设计器<br />-Web 设计器和 HTML 编辑器|  
|数据|-   **服务器资源管理器**(简化： 仅限数据)。 请参阅备注 1。<br />-   **数据源**窗口<br />的组完整的数据控件<br />XML 编辑器<br />数据绑定到本地数据源 (。MDF 或。MDB)<br />数据绑定到对象<br />数据绑定到 Web 服务<br />数据绑定到本地数据库服务器<br />数据绑定到远程数据库服务器<br />远程数据的 DDL 工具<br />-   **服务器资源管理器**扩展性 ([!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]示例)|  
|调试器|-本地调试。 请参阅备注 2。<br />-托管调试<br />-本地调试<br />附加到的本地进程<br />附加到的远程进程<br />匿名委托<br />-应用程序域<br />-ASPX 调试<br />-属性<br />-中断在 Func 评估过程<br />-断点<br />-断点约束<br />-调用堆栈<br />-   **命令**窗口<br />-跨线程调试<br />数据提示<br />数据可视化工具<br />托管调试助手 (Mda) 的集成调试器支持<br />的类型转发器调试器支持<br />-对 OTB DTEEvents 支持<br />-   JMC Stepper<br />-调试器 AppID 测试 (DBGCLR)<br />调试程序配置文件<br />-调试器的工具和选项<br />调试迭代器<br />-设计时表达式计算<br />-C# 表达式计算器<br />-反汇编<br />-编辑并继续<br />表达式计算器 windows （Watch 局部变量，自动)<br />-异常帮助器<br />-异常<br />执行<br />-   泛型<br />-获取正确的源<br />HPC/群集调试<br />集成多语言调试<br />-互操作调试<br />-在实时调试<br />-本地调试<br />-托管调试<br />-手动控制 （进程窗口）<br />-内存<br />-小型转储支持<br />-模块<br />-多进程调试<br />本机调试<br />-新调试引擎支持<br />-优化的代码调试<br />的筛选输出窗口<br />-进程承载托管调试<br />-进程<br />-快速监视<br />-注册<br />的堆栈中寄存器<br />-远程调试<br />-返回值<br />脚本调试<br />源服务支持<br />-安全<br />--并排方案<br />-   SQL<br />符号服务器<br />-跟踪点<br />线程<br />-可视化效果<br />可扩展样式表语言转换 (XSLT) 调试器|  
|64 位支持|-对于托管和本机代码，所有语言调试 64 位<br />-x64 本机支持|  
|源代码管理 (SCC)|-基本源代码管理集成。 请参阅备注 3。<br />-工具和选项验证|  
|扩展性|使用 Vspackage 和 MEF 组件|  
  
## <a name="notes"></a>说明  
  
#### <a name="1-data-tools"></a>1.数据工具  
 集成的 shell 包括数据库开发工具，例如数据扩展性支持和简化**解决方案资源管理器**。 但是，SQL Server Express、 SQL Reporting，和 Crystal Reports 不包含在集成外壳。  
  
#### <a name="2-debugging-support"></a>2.调试支持  
 集成的 shell 包括相同的 Visual Studio 社区版中包含的调试引擎。 调试引擎包含公共调试器托管的代码中，以及相关的功能，例如运行、 附加、 设置断点、 编辑并继续，以及其他人。 但是，调试引擎不支持 SQL Server 数据库调试。  
  
 尽管支持的基本调试器包中包括本机调试，不能进行扩展以支持其他语言。  
  
#### <a name="3-source-code-control-integration"></a>3.源代码管理集成  
 集成的外壳提供了 Api，用于实现源代码管理 (SCC) 和提供的 MSSCCI 基于常见的源控件集成组件。  
  
 虽然 SCC 集成不专业版的 Visual Studio 的一项常规功能，但集成外壳提供源代码管理集成。  
  
#### <a name="4-build-support"></a>4.生成支持  
 集成的外壳提供生成支持。 您可以找到有关在生成的信息[MSBuild 引用](../msbuild/msbuild-reference.md)。  
  
## <a name="features-not-included-in-the-integrated-shell"></a>不包括在集成 Shell 中的功能  
 下面是不包括在集成 shell 的功能的列表：  
  
- 类设计器  
  
- PreEmptive Protection - Dotfuscator  
  
- 语言功能  
  
- VSHost  
  
- 没有 Visual Studio 语言或其关联的项目模板或项目项模板包含在集成 shell 中。 用于示例的 Visual Basic 代码段中包含的其他功能没有特定于语言的实现。  
  
## <a name="see-also"></a>请参阅  
 [扩展 Visual Studio 概述](https://msdn.microsoft.com/library/3e9078d7-2763-4cc4-8e20-fac69d747f59)