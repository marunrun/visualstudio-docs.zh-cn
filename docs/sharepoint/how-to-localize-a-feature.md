---
title: 如何：本地化功能 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- features [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b0d15654ba48b6c95cf2b2f7fa4f9cd665f0959a
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016140"
---
# <a name="how-to-localize-a-feature"></a>如何：本地化功能
  默认情况下，功能标题和说明使用硬编码的字符串值。 若要本地化功能标题和说明，请将字符串替换为引用本地化资源的表达式。

## <a name="localize-a-feature"></a>本地化功能

#### <a name="to-localize-a-feature"></a>本地化功能

1. 在**解决方案资源管理器**中，打开**Feature1**节点的快捷菜单，然后选择 "**添加功能资源**"。

2. 在 "**添加资源**" 对话框中，从列表中选择 "**固定语言**" 作为 "默认语言" 功能资源文件的区域性。

3. 对每种本地化语言重复先前的步骤，同时对本地化的功能资源文件选择所需的语言。

     将创建单独的功能资源文件：一个用于默认语言，另一个用于您希望支持的每种本地化语言。

4. 在资源编辑器中打开每个资源文件，并输入所有字符串 ID 及其值。

     例如，在默认的功能资源文件中，输入一个标题值为 **"我的功能标题**" 的**标题**，并输入一个值为 **"我的功能说明**" 的**说明**的第二个字符串 id。 对于每个本地化的资源文件，使用默认功能资源文件中所使用的相同字符串 ID，但为值输入本地化的字符串。

5. 输入所有资源值后，打开功能的快捷菜单（例如， *Feature1*），然后选择 "**查看设计器**" 以打开功能设计器中的功能。

6. 若要本地化功能中的 "**标题**" 和 "**说明**" 字段，请使用以下格式在其框中输入值：

     `$Resources:` *字符串 ID*

     例如，在**功能标题**框中输入 $Resources：**Title** ，并 $Resources： "**功能说明**" 框中的 "**说明**"。

     字符串 ID 必须与资源文件中使用的字符串 ID 匹配。

7. 选择**F5**键生成并运行应用程序。

8. 在 SharePoint 中，打开 "**站点操作**" 菜单，选择 "**站点设置**"，然后在 "**站点操作**" 部分中选择 "**管理站点功能**" 链接。

9. 在 SharePoint 中，从默认值更改显示语言。

     本地化功能标题和说明显示在应用程序中。 若要显示本地化的资源，SharePoint 服务器必须安装与资源文件的区域性匹配的语言包。

## <a name="see-also"></a>另请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
