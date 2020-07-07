---
title: 如何：将控件标记为安全控件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, safe controls
- SharePoint development in Visual Studio, advanced packaging tools
- safe controls [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: cd7ed13504d3d91f4239a8ea070454e1c31b1114
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016257"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>如何：将控件标记为安全控件
  为安全，SharePoint 在保护的 Web 控件和不是的脚本注入和 Web 控件之间区分开来。 不受信任的用户可以访问受保护的控件或*安全控件*。 将程序集添加到包中时，可以在 SharePoint 项目项的 "安全控件项" 属性或**包设计器**中将控件标记为安全。 有关详细信息，请参阅

- [web.config 文件设置更改并将](/previous-versions/office/developer/sharepoint-2007/bb802890(v=office.12)) [Web 部件程序集注册为安全控件](/previous-versions/office/developer/sharepoint2003/dd587360(v=office.11))。

> [!IMPORTANT]
> 这些过程用于说明目的。 仅在确定控件安全时才将其标记为安全。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>在 "安全控件项" 属性中标记安全控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>将控件标记为安全控件项属性中的安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

3. 将两个项添加到 Web 部件的 "**安全控件项**" 属性中。 为此，请在 "**属性**" 窗口中选择 "**安全控件项**" 属性旁边的省略号（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮。

     此时将显示 "**安全控制条目**" 对话框。

4. 在 "**安全控件项**" 对话框中，选择 "**添加**" 按钮两次，将两个安全控件项添加到 "**成员**" 窗格中：一个用于按钮，一个用于文本框。

5. 选择第一个 "安全控制" 项，然后将其 "**安全**" 属性的值更改为 " **false**"，将其 "**类型名称**" 属性更改为 " **Button1**"，并将其 "**安全**" 设置为 " **false**"

     此步骤将按钮控件标识为不安全控件。

6. 选择列表中的第二个安全控件项。 将其**Safe**属性的值保留为**true** ，并将其 "**类型名称**" 属性设置为 " **TextBox1** "，并将其 "**安全应对脚本**" 属性设置为**true**。

     文本框控件现在被标记为可安全应对脚本注入的控件。

7. 选择“确定”按钮关闭对话框。

## <a name="marking-safe-controls-in-the-package-designer"></a>在包设计器中标记安全控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>在包设计器中将控件标记为安全或不安全

1. 使用可视 Web 部件项目创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件：文本框和按钮。 将名称分别保留为默认值 TextBox1 和 Button1。

     记下控件的命名空间，因为稍后将用到它。

3. 在菜单栏上，选择 "**生成**" "生成  >  **解决方案**" 以生成项目。

4. 创建另一个 SharePoint 解决方案。

5. 在**解决方案资源管理器**中，打开*包*文件的快捷菜单，然后选择 "**打开**" 以打开**包设计器**。

6. 在**包设计器**中，选择 "**高级**" 选项卡。

7. 在 "**其他程序集**" 下，选择 "**添加**" 按钮，然后从列表中选择 "**添加现有程序集**"。

8. 在 "**添加现有程序集**" 对话框中，选择 "**源路径**" 旁边的省略号（![ASP.NET Mobile 设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮。

9. 从你在步骤1中创建的 SharePoint 解决方案中选择程序集，然后选择 "**打开**" 按钮。

10. 对于本示例，请将 "**部署目标**" 选项保留为 "GlobalAssemblyCache"。

     此步骤将导致程序集部署到系统全局程序集缓存（GAC）。 如果希望程序集部署到 Web 应用程序（Bin）文件夹，请改为选择该选项。 有关详细信息，请参阅[在 SharePoint Foundation 中部署 Web 部件](/previous-versions/office/developer/sharepoint-2010/cc768621(v=office.14))。

11. 在 "**安全控件**" 框中，选择 "**单击此处添加新项**" 按钮。

12. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如**BdcModelProject1. VisualWebPart1**。|
    |类型名称|Button1|
    |程序集名称|强程序集名称，例如： ClientExtensions、Version = 14.0.0.0、Culture = 中立、PublicKeyToken = 71e9bce111e9429c。|
    |Safe|清除 "**安全**" 复选框。|
    |安全应对脚本|清除 "**安全应对脚本**" 复选框。|

    > [!NOTE]
    > 通过**包设计器**的 "**高级**" 选项卡添加的程序**集的程序集名称**值不能是标记，它必须是具有强名称的程序集。 有关详细信息，请参阅[创建和使用具有强名称的程序集](/previous-versions/dotnet/netframework-4.0/xwb8f617(v=vs.100))。

13. 选择**Tab**键以创建另一个安全控件项。

14. 再次选择 "**单击此处添加新项"** 按钮。

15. 输入下表中属性的值。

    |属性名称|Value|
    |-------------------|-----------|
    |命名空间|控件的完全限定命名空间，例如**BdcModelProject1. VisualWebPart1**。|
    |类型名称|TextBox1|
    |程序集名称|强程序集名称，例如： ClientExtensions、Version = 14.0.0.0、Culture = 中立、PublicKeyToken = 71e9bce111e9429c。|
    |Safe|选中 "**安全**" 复选框。|
    |安全应对脚本|选中 "**安全应对脚本**" 复选框。|

16. 选择**Tab**键，然后选择 "**确定"** 按钮关闭对话框。

## <a name="see-also"></a>另请参阅
- [在项目项中提供打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
