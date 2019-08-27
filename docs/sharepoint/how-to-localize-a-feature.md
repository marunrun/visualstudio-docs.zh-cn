---
title: 如何：本地化功能 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: f6e796cc00478ee823c345fd02738f8677c36373
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813662"
---
# <a name="how-to-localize-a-feature"></a>如何：本地化功能
  默认情况下，功能标题和说明使用硬编码的字符串值。 若要本地化的功能标题和说明，请使用表达式引用本地化的资源的替换字符串。

## <a name="localize-a-feature"></a>本地化功能

#### <a name="to-localize-a-feature"></a>若要本地化功能

1. 在中**解决方案资源管理器**，打开快捷菜单**Feature1**节点，然后选择**添加功能资源**。

2. 在中**添加资源**对话框框中，选择**固定语言**从作为默认语言功能资源文件的区域性列表。

3. 对每种本地化语言重复先前的步骤，同时对本地化的功能资源文件选择所需的语言。

     将创建单独的功能资源文件：一个用于默认语言，另一个用于您希望支持的每种本地化语言。

4. 在资源编辑器中打开每个资源文件，并输入所有字符串 ID 及其值。

     例如，在默认功能资源文件中，输入的字符串 ID**标题**值为**My 功能标题**，以及第二个字符串的 ID**说明**值为**我的功能说明**。 对于每个本地化的资源文件，使用默认功能资源文件中所使用的相同字符串 ID，但为值输入本地化的字符串。

5. 输入所有资源值后，打开快捷菜单的功能 (例如， *Feature1.feature*)，然后选择**视图设计器**在功能设计器中打开该功能。

6. 若要本地化**标题**并**说明**字段在功能中，使用以下格式在其框中输入值：

     `$Resources:` *字符串 ID*

     例如，输入 $Resources:**标题**中**功能标题**框中和 $Resources:**说明**中**功能说明**框.

     字符串 ID 必须与资源文件中使用的字符串 ID 匹配。

7. 选择**F5**键生成并运行应用程序。

8. 在 SharePoint 中，打开**站点操作**菜单中，选择**站点设置**，然后在**站点操作**部分中选择**管理站点功能**链接。

9. 在 SharePoint 中，更改默认的显示语言。

     应用程序中出现的本地化的功能标题和说明。 若要显示的本地化的资源，SharePoint 服务器必须具有匹配资源文件的区域性的语言包安装。

## <a name="see-also"></a>请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
