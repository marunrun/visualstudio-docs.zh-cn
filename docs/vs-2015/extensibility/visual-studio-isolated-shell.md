---
title: Visual Studio 独立 Shell |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], shell-based applications%2C isolated mode
- Visual Studio shell, isolated mode
- isolated shell-based applications [Visual Studio]
- Visual Studio shell, shell-based applications%2C isolated mode
- Shell [Visual Studio], isolated mode
ms.assetid: d2620e71-be9e-44c9-b5b7-03a4c8d9cf0b
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0309019cc36e9f81596061dbbede0f84b0b78a05
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403585"
---
# <a name="visual-studio-isolated-shell"></a>Visual Studio 独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 独立 shell，可创建独立的应用程序可以运行的同时与其他版本的 Visual Studio。 它是主要用于托管专用的工具，可以使用 Visual Studio 服务，但还具有自定义的外观和品牌。 Visual Studio 功能和菜单命令组可以轻松地打开和关闭。 完全可自定义应用程序标题、 应用程序图标和初始屏幕。 可自定义功能的列表，请参阅[自定义独立 Shell](../extensibility/customizing-the-isolated-shell.md)。  
  
 若要使用的独立的 shell 项目，必须安装 Visual Studio SDK。 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
 若要创建独立的 shell 应用程序，请使用 Visual Studio Shell 独立项目开始。 此项目包含你开发和测试独立的 shell 应用程序所需的所有内容。 若要编写部署你的应用程序安装程序准备就绪后，必须获取从独立的 shell 可再发行组件包[Microsoft Visual Studio Shell （独立） Redistributable Package](http://go.microsoft.com/fwlink/?LinkId=616022)。  
  
> [!NOTE]
> 在可以访问独立的 shell 可再发行组件包之前，系统将要求填写份简短的客户调查。  填写调查之后, 你将定向到 Visual Studio Connect 页面使用可再发行组件包下载链接。  可以在以后访问下的 Visual Studio Connect 站点上找到的下载链接**程序&#124;VISUAL STUDIO 2015 集成和独立 SHELL**选项卡。  
  
> [!NOTE]
> 有关如何部署独立的基于 shell 的应用程序的详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="working-with-the-isolated-shell"></a>使用独立 shell  
 Visual Studio 独立 shell 应用程序具有对 Visual Studio 服务的完全访问权限，并支持特殊的自定义和品牌。 有几种方法可以自定义独立的 shell 应用程序：  
  
- Vspackage 和 Managed Extensibility Framework (MEF) 组件部分可用于扩展独立的 shell 的应用程序，就像任何其他 Visual Studio 扩展中使用它们。 有关详细信息，请参阅[扩展独立 Shell](../extensibility/extending-the-isolated-shell.md)。  
  
- 若要使 Visual Studio 功能和菜单命令组可用或不可用，请更新应用程序的用户界面 (UI) 项目中的.vsct 文件。  
  
- 若要删除**选项**页面或应用程序，其他 Visual Studio shell 组件更新.pkgundef 文件的应用程序。  
  
- 若要修改其他方面的外观或行为的 shell，请更新应用程序的.pkgdef 文件。  
  
- 启动应用程序时，还可以指定外壳程序的某些方面。 若要执行此操作，更新到 appenvstub.dll 的启动入口点调用中的参数。  
  
  有关可以自定义的不同元素的详细信息，请参阅[独立 Shell 的元素](../extensibility/elements-of-the-isolated-shell.md)。  
  
## <a name="standard-features-of-the-isolated-shell"></a>标准功能的独立 Shell  
 以下功能是对所有版本的 Visual Studio 标准。  
  
|功能类别|功能|  
|----------------------|-------------|  
|IDE 功能|导入/导出设置<br /><br /> 工具箱控件安装程序<br /><br /> 任务列表和错误列表<br /><br /> 输出窗口<br /><br /> 起始页<br /><br /> 属性窗口<br /><br /> 工具箱<br /><br /> “解决方案资源管理器”<br /><br /> “书签”窗口<br /><br /> 类视图<br /><br /> 对象浏览器<br /><br /> “命令”窗口<br /><br /> 文档大纲<br /><br /> 资源视图<br /><br /> 外部工具<br /><br /> Windows Communication Foundation (WCF) 添加服务引用<br /><br /> 语言集成查询 (LINQ) 支持|  
|编辑器/设计器|代码浏览工具 （统一的查找、 源定义，继承）<br /><br /> IntelliSense<br /><br /> SmartTags<br /><br /> 代码片段管理器<br /><br /> 代码段<br /><br /> 重构<br /><br /> 整齐排列<br /><br /> IntelliSense 筛选<br /><br /> “代码定义”窗口<br /><br /> 应用程序设计器<br /><br /> Windows Forms Designer — Windows 窗体设计器<br /><br /> Windows Presentation Foundation (WPF) 设计器|  
|调试|C# 表达式计算器<br /><br /> 本地调试<br /><br /> 托管调试<br /><br /> 编辑并继续<br /><br /> 跨线程调试<br /><br /> 可视化效果<br /><br /> 数据提示<br /><br /> 本机调试<br /><br /> 脚本调试<br /><br /> 互操作调试<br /><br /> 实时 (JIT) 调试<br /><br /> 多进程调试<br /><br /> XSLT 调试<br /><br /> 附加到本地进程<br /><br /> 跟踪点<br /><br /> 断点约束|  
|数据|服务器资源管理器 （简体-仅限数据）<br /><br /> 将数据绑定到本地数据 (。MDF 或。MDB)<br /><br /> 数据绑定到对象<br /><br /> 数据绑定到 Web 服务<br /><br /> 完整的数据控件集<br /><br /> XML 编辑器<br /><br /> 将数据绑定到本地数据库服务器<br /><br /> “数据源”窗口|  
|Web|HTML 编辑器<br /><br /> Web 浏览器<br /><br /> Web 窗体设计器<br /><br /> 网站项目<br /><br /> Web 应用程序项目|  
|扩展性|使用 Vspackage 和 MEF 组件|  
  
## <a name="see-also"></a>请参阅  
 [Shell（独立或集成）](../extensibility/shell-isolated-or-integrated.md)
