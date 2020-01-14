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
ms.openlocfilehash: ef2d1cbffab5e38e603b0e50beb896f1c6efa23d
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919202"
---
# <a name="visual-studio-isolated-shell"></a>Visual Studio 独立 Shell
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

借助 Visual Studio 独立 Shell，您可以创建能与其他 Visual Studio 版本并行运行的独立应用程序。 它主要用于托管可使用 Visual Studio 服务的专用工具，还可具有自定义外观和品牌。 可以轻松打开和关闭 Visual Studio 功能和菜单命令组。 应用程序标题、应用程序图标和初始屏幕都是可完全自定义的。 有关可自定义功能的列表，请参阅[自定义独立 Shell](../extensibility/customizing-the-isolated-shell.md)。  
  
 若要使用独立 shell 项目，必须安装 Visual Studio SDK。 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
 若要创建独立 shell 应用程序，请首先使用 Visual Studio Shell 独立项目。 此项目包含开发和测试自己的独立 shell 应用程序所需的所有内容。 准备好编写部署应用程序的安装程序时，必须从[Microsoft Visual Studio Shell (独立) 可再发行组件包](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)获取隔离 shell 可再发行组件包。  
  
> [!NOTE]
> 你需要先填写一份简短的客户调查，然后才能访问隔离 shell 可再发行组件包。  填写完客户调查后，您会转到包含可再发行组件包下载链接的 Visual Studio Connect 页面。  可以在后续访问 visual studio **2015 集成和隔离 SHELL &#124;** 选项卡下的 visual studio Connect 站点时找到下载链接。  
  
> [!NOTE]
> 有关如何部署基于 shell 的独立应用程序的详细信息，请参阅[演练：创建基本的独立 Shell 应用程序](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)。  
  
## <a name="working-with-the-isolated-shell"></a>使用独立 shell  
 Visual Studio 独立 shell 应用程序具有对 Visual Studio 服务的完全访问权限，并支持特殊的自定义和品牌。 可以通过多种方式自定义独立 shell 应用程序：  
  
- 您可以使用 Vspackage 和 Managed Extensibility Framework （MEF）组件部分来扩展独立 shell 应用程序，就像在任何其他 Visual Studio 扩展中使用一样。 有关详细信息，请参阅[扩展独立 Shell](../extensibility/extending-the-isolated-shell.md)。  
  
- 若要使 Visual Studio 功能和菜单命令组可用或不可用，请更新应用程序的用户界面（UI）项目中的 .vsct 文件。  
  
- 若要从应用程序中删除**选项**页或其他 Visual Studio shell 组件，请更新应用程序的 .pkgundef 文件。  
  
- 若要修改 shell 的外观或行为的其他方面，请更新应用程序的 .pkgdef 文件。  
  
- 在应用程序启动时，还可以指定 shell 的某些方面。 为此，请将调用中的参数更新到 appenvstub 的开始入口点。  
  
  有关可自定义的不同元素的详细信息，请参阅[独立 Shell 的元素](../extensibility/elements-of-the-isolated-shell.md)。  
  
## <a name="standard-features-of-the-isolated-shell"></a>独立 Shell 的标准功能  
 以下功能适用于所有版本的 Visual Studio。  
  
|功能类别|功能|  
|----------------------|-------------|  
|IDE 功能|导入/导出设置<br /><br /> 工具箱控件安装程序<br /><br /> 任务列表 & 错误列表<br /><br /> “输出”窗口<br /><br /> 起始页<br /><br /> 属性窗口<br /><br /> 工具箱<br /><br /> “解决方案资源管理器”<br /><br /> “书签”窗口<br /><br /> 类视图<br /><br /> 对象浏览器<br /><br /> “命令”窗口<br /><br /> 文档大纲<br /><br /> 资源视图<br /><br /> 外部工具<br /><br /> Windows Communication Foundation （WCF）添加服务引用<br /><br /> 语言集成查询（LINQ）支持|  
|编辑器/设计器|代码浏览工具（统一查找、源定义、继承）<br /><br /> IntelliSense<br /><br /> SmartTags<br /><br /> 代码片段管理器<br /><br /> 代码片段<br /><br /> Refactoring<br /><br /> 整齐列出<br /><br /> IntelliSense 筛选<br /><br /> “代码定义”窗口<br /><br /> 应用程序设计器<br /><br /> Windows Forms Designer — Windows 窗体设计器<br /><br /> Windows Presentation Foundation （WPF）设计器|  
|调试|C#表达式计算器<br /><br /> 本地调试<br /><br /> 托管调试<br /><br /> 编辑并继续<br /><br /> 跨线程调试<br /><br /> 可视化效果<br /><br /> 数据提示<br /><br /> 本机调试<br /><br /> 脚本调试<br /><br /> 互操作调试<br /><br /> 实时（JIT）调试<br /><br /> 多进程调试<br /><br /> XSLT 调试<br /><br /> 附加到本地进程<br /><br /> 跟踪点<br /><br /> 断点约束|  
|数据|服务器资源管理器（仅限简体中文）<br /><br /> 数据绑定到本地数据（.MDF 或.MDB<br /><br /> 数据绑定到对象<br /><br /> 数据绑定到 Web 服务<br /><br /> 完整的数据控件集<br /><br /> XML 编辑器<br /><br /> 数据绑定到本地数据库服务器<br /><br /> “数据源”窗口|  
|Web|HTML 编辑器<br /><br /> Web 浏览器<br /><br /> Web 窗体设计器<br /><br /> 网站项目<br /><br /> Web 应用程序项目|  
|可扩展性|使用 Vspackage 和 MEF 组件|  
  
## <a name="see-also"></a>请参阅  
 [Shell（独立或集成）](../extensibility/shell-isolated-or-integrated.md)
