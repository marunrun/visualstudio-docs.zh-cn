---
title: 如何：本地化 ASPX 标记 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4cd3c17a9e771ad9a1aee7526f24e3a8282f208d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443105"
---
# <a name="how-to-localize-aspx-markup"></a>如何：本地化 ASPX 标记
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) 页通常使用硬编码的字符串值。 若要本地化这些字符串，这些替换表达式引用本地化的资源。

## <a name="localize-aspx-markup"></a>本地化 ASPX 标记

#### <a name="to-localize-aspx-markup"></a>若要本地化 ASPX 标记

1. 添加单独的资源文件： 一个默认语言，一个用于每个本地化语言。

     如果您要本地化仅标记并不是代码，添加全局资源文件项目项。 如果您要本地化代码和标记，添加资源文件项目项。

    1. 若要在中添加全局资源文件，请**解决方案资源管理器**，打开 SharePoint 项目项的快捷菜单，然后选择**添加** > **新项**。 在 SharePoint 下**2010年**节点，选择**全局资源文件**模板。

    2. 若要添加的资源文件，在**解决方案资源管理器**，打开 SharePoint 项目项的快捷菜单，然后选择**添加** > **新项**。 下**Visual Basic**或**Visual C#** 节点，选择**资源文件**模板。

    > [!NOTE]
    > 请确保将资源文件添加到 SharePoint 项目项以启用部署类型属性。 稍后在此过程需要此属性。 如果你的解决方案不具有 SharePoint 项目项，您可以添加一个空 SharePoint 项目和删除其默认值*Elements.xml*文件。

2. 为追加与所选的指定名称的默认语言资源文件 *.resx*扩展名，例如 MyAppResources.resx。 对每个本地化资源文件使用同一基名称，但添加区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，本地化资源名称德语*MyAppResources.de-DE.resx*。

3. 更改的值**部署类型**到每个资源文件的属性**AppGlobalResource**以使其部署到服务器的 App_GlobalResources 文件夹。

4. 如果使用的资源来本地化除 ASPX 标记之外的代码，保留值**生成操作**属性的每个文件作为**嵌入的资源**。 如果使用的资源文件来本地化标记，可以根据需要更改的文件的属性值**内容**。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

5. 打开每个资源文件并添加已本地化的字符串，每个文件中使用的相同字符串 Id。

6. 在[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]标记 ASPX 页或控件，将使用以下格式的值替换为硬编码的字符串：

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     例如，若要本地化的应用程序页上的标签控件的文本，请更改：

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     更改为

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. 选择**F5**键生成并运行应用程序。

8. 在 SharePoint 中，更改默认的显示语言。

     应用程序中出现的本地化的字符串。 若要显示的本地化的资源，SharePoint 服务器必须具有匹配资源文件的区域性的语言包安装。

## <a name="see-also"></a>请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
