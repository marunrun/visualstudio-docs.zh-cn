---
title: 如何：本地化 ASPX 标记 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: 63bd8ee614a78752069002820689a2cc6c0be783
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016280"
---
# <a name="how-to-localize-aspx-markup"></a>如何：本地化 ASPX 标记
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)]（.aspx）页通常使用硬编码的字符串值。 若要对这些字符串进行本地化，请将其替换为引用本地化资源的表达式。

## <a name="localize-aspx-markup"></a>本地化 ASPX 标记

#### <a name="to-localize-aspx-markup"></a>本地化 ASPX 标记

1. 添加单独的资源文件：一个用于默认语言，另一个用于每个本地化语言。

     如果仅本地化标记而不是代码，请添加 "全局资源文件" 项目项。 如果要本地化代码和标记，请添加 "资源文件" 项目项。

    1. 若要添加全局资源文件，请在**解决方案资源管理器**中，打开 SharePoint 项目项的快捷菜单，然后选择 "**添加**  >  **新项**"。 在 SharePoint **2010**节点下，选择 "**全局资源文件**" 模板。

    2. 若要添加资源文件，请在**解决方案资源管理器**中，打开 SharePoint 项目项的快捷菜单，然后选择 "**添加**  >  **新项**"。 在 " **Visual Basic** " 或 " **Visual c #** " 节点下，选择 "**资源文件**" 模板。

    > [!NOTE]
    > 请确保将资源文件添加到 SharePoint 项目项，以启用 "部署类型" 属性。 此属性稍后在此过程中需要此属性。 如果你的解决方案没有 SharePoint 项目项，则可以添加一个空 SharePoint 项目，并删除其默认的*Elements.xml*文件。

2. 为默认语言资源文件指定您选择的名称，并以 *.resx*扩展名（如 MyAppResources）追加。 对每个本地化资源文件使用同一基名称，但添加区域性 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，将德语本地化资源命名为*MyAppResources.de*。

3. 将每个资源文件的 "**部署类型**" 属性的值更改为**AppGlobalResource** ，使其部署到服务器的 App_GlobalResources 文件夹。

4. 如果使用资源来本地化除 ASPX 标记之外的代码，请将每个文件的 "**生成操作**" 属性的值保留为**嵌入的资源**。 如果只使用资源文件来本地化标记，则可以选择将文件的属性值更改为 "**内容**"。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

5. 打开每个资源文件，并在每个文件中使用相同的字符串 Id 来添加已本地化的字符串。

6. 在 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ASPX 页或控件的标记中，将硬编码字符串替换为以下格式的值：

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     例如，若要在应用程序页上本地化 "标签" 控件的文本，将更改：

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     to

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. 选择**F5**键生成并运行应用程序。

8. 在 SharePoint 中，从默认值更改显示语言。

     本地化的字符串将显示在应用程序中。 若要显示本地化的资源，SharePoint 服务器必须安装与资源文件的区域性匹配的语言包。

## <a name="see-also"></a>另请参阅
- [本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)
- [如何：本地化功能](../sharepoint/how-to-localize-a-feature.md)
- [如何：添加资源文件](../sharepoint/how-to-add-a-resource-file.md)
- [如何：本地化代码](../sharepoint/how-to-localize-code.md)
