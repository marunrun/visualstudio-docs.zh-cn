---
title: 如何：本地化代码 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8b848bdb4d0b71f5762601204195f0e81a1c2733
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443084"
---
# <a name="how-to-localize-code"></a>如何：本地化代码
  未本地化的代码使用硬编码的字符串值。 若要本地化代码字符串，将其替换为对调用<xref:System.Web.HttpContext.GetGlobalResourceObject%2A>，这是引用本地化的资源的方法。

## <a name="localize-code"></a>本地化代码

#### <a name="to-localize-code"></a>若要本地化代码

1. 在中**解决方案资源管理器**，打开项目项的快捷菜单，然后选择**添加** > **模块**。

     选择**资源文件**模板。

    > [!NOTE]
    > 请确保将资源文件添加到 SharePoint 项目项，以便部署类型属性。 稍后在此过程需要此属性。

2. 为追加与所选的指定名称的默认语言资源文件 *.resx*扩展，如*MyAppResources.resx*。

3. 重复步骤 1 和步骤 2，向 SharePoint 项目项添加单独的资源文件：每种本地化语言各对应一个文件。

     使用相同的基名称为每个本地化的资源文件，但添加区域性 id。 例如，本地化资源名称德语*MyAppResources.de-DE.resx*。

4. 打开每个资源文件并添加已本地化的字符串。 在每个文件中使用相同的字符串 ID。

5. 更改的值**部署类型**到每个资源文件的属性**AppGlobalResource**以使每个文件将部署到服务器的 App_GlobalResources 文件夹。

6. 保留值**生成操作**属性的每个文件作为**嵌入的资源**。

     嵌入的资源将编译到项目的 DLL 中。

7. 生成项目以创建资源附属 Dll。

8. 在中**包设计器**，选择**高级**选项卡上，以及如何将附属程序集。

9. 在中**位置**框中，在前面添加区域性 ID 文件夹在位置路径，如*DE-DE\\\<项目项名称 >。 resources.dll*。

10. 如果你的解决方案已引用 System.Web 程序集，添加的引用，并将指令添加到代码中<xref:System.Web>。

11. 在你的代码中找到用户可见的所有硬编码的字符串，如 UI 文本、错误和消息文本。 使用以下语法将这些字符串替换为对 <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> 方法的调用：

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. 选择**F5**键生成并运行应用程序。

13. 在 SharePoint 中，更改默认的显示语言。

     应用程序中出现的本地化的字符串。 若要显示的本地化的资源，SharePoint 服务器必须具有匹配资源文件的区域性的语言包安装。

## <a name="see-also"></a>请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：本地化 ASPX 标记](../sharepoint/how-to-localize-aspx-markup.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
