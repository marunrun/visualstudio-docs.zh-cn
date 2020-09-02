---
title: "\"URL 选取器\" 对话框 (SharePoint 开发) "
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.VWD.URLPicker
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, URL picker
- SharePoint development in Visual Studio, designer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 991693c3379e008a2a907efd3127290c7e804c22
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66261946"
---
# <a name="url-picker-dialog-box-sharepoint-development-in-visual-studio"></a>"URL 选取器" 对话框 (Visual Studio 中的 SharePoint 开发) 
  在“URL 选取器”对话框中，您可以选择文件，如位于项目中或运行 SharePoint 的本地服务器上的母版页文件或图像文件。

 在能够选择某个文件以设置属性时，将会显示该对话框。 可以通过选择 "**属性**" 窗口中各种属性旁的省略号按钮 (![ASP.NET Mobile 设计器](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")") 来打开此对话框。 在设计器的 " **源** " 视图中向某些属性赋值时，省略号按钮还显示为 IntelliSense 提示符。

## <a name="uielement-list"></a>UIElement 列表
 **项目文件夹** 显示在项目中或在运行 SharePoint 的本地服务器上定义的文件夹的列表。 选择展开按钮可显示子文件夹。

 展开 **项目** 节点以选择项目中的文件。 若要在对话框中显示为可选择，项目中的文件必须满足以下条件：

- 文件必须包含在映射文件夹中。

- 必须将该文件添加到解决方案包。

- 该文件不能位于另一个项目中。

  如果要引用不满足这些条件的文件，则必须手动输入文件的路径。

  展开 **服务器** 节点，选择位于运行 SharePoint 的本地服务器上的文件。 若要在对话框中显示为可选择，这些文件必须满足以下条件：

- 该文件必须位于以下映射文件夹之一中： **图像**、 **布局**或 **ControlTemplates**。

- 无法在 SharePoint 内容数据库中找到该文件。

  如果要引用不满足这些条件的文件，则必须手动输入文件的路径。

  **文件夹内容** 显示选定文件夹中的文件的列表。 选择一个文件，然后选择 " **确定"** 按钮以关闭对话框并将所选内容发送到调用它的进程。

  **文件类型** 允许从适合于正在执行的任务的文件列表中进行选择。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [为 SharePoint 创建 web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [为 web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
