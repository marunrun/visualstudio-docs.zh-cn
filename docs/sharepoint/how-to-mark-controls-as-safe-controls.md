---
title: 如何：将控件标记为安全控件 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 30bb597288c19328bb71ce7b5212200991d7181e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443072"
---
# <a name="how-to-mark-controls-as-safe-controls"></a>如何：将控件标记为安全控件
  为了安全，SharePoint 区分防止脚本注入的 Web 控件和 Web 控件不是。 受保护的控件，或*安全控件*，可以由不受信任的用户访问。 您可以将标记为安全控件项属性的 SharePoint 项目项中或在中安全控件**包设计器**时向包中添加程序集。 有关详细信息，请参见

- [web.config 文件设置更改](http://go.microsoft.com/fwlink/?LinkId=178965)并[Web 部件程序集注册为安全控件](http://go.microsoft.com/fwlink/?LinkId=171013)。

> [!IMPORTANT]
> 这些过程是用于说明目的。 仅当你确信它们是安全的安全控件标记。

## <a name="marking-safe-controls-in-the-safe-control-entries-property"></a>将标记为安全控件条目属性中的安全控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-safe-control-entries-property"></a>若要将控件标记为安全或不安全的安全控件项属性

1. 使用 Visual Web 部件项目中创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件： 一个文本框和一个按钮。 分别将 TextBox1 和 Button1，其默认值保留的名称。

3. 将两个条目添加到 Web 部件**安全控件项**属性。 若要执行此操作，请选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮旁边**安全控件项**中的属性**属性**窗口。

     **安全控件项**对话框随即出现。

4. 在**安全控件项**对话框框中，选择**添加**按钮两次以添加两个安全控件条目**成员**窗格： 一个用于按钮和一个用于文本框。

5. 选择第一个安全控件项，然后更改的值及其**安全**属性设置为**False**，将其**类型名称**属性设置为**Button1**，并将其**安全应对脚本**属性设置为**False**。

     此步骤中标识为不安全的控件的按钮控件。

6. 选择列表中的第二个安全控件项。 保留的值及其**安全**属性作为**True**并设置其**类型名称**属性设置为**TextBox1**并将其**安全对脚本**属性设置为**True**。

     文本框控件现在标记为可安全应对脚本注入的控件。

7. 选择“确定”  按钮关闭对话框。

## <a name="marking-safe-controls-in-the-package-designer"></a>标记在包设计器中的安全控件

#### <a name="to-mark-controls-as-safe-or-unsafe-in-the-package-designer"></a>将控件标记为安全或不安全的包设计器

1. 使用 Visual Web 部件项目中创建 SharePoint 解决方案。

2. 将两个控件添加到 Web 部件： 一个文本框和一个按钮。 分别将 TextBox1 和 Button1，其默认值保留的名称。

     记控件的命名空间，因为它使用更高版本。

3. 在菜单栏上依次选择**构建** > **生成解决方案**以生成项目。

4. 创建另一个 SharePoint 解决方案。

5. 在中**解决方案资源管理器**，打开快捷菜单*Package.Package*文件，，然后选择**打开**以打开**包设计器**.

6. 在中**包设计器**，选择**高级**选项卡。

7. 下**其他程序集**，选择**添加**按钮，，然后选择**添加现有程序集**从列表中。

8. 在中**添加现有程序集**对话框框中，选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮旁边**源路径**。

9. 从你在步骤 1 中创建 SharePoint 解决方案中选择程序集，然后选择**打开**按钮。

10. 此示例中，将保留**部署目标**GlobalAssemblyCache 选项。

     此步骤会导致程序集部署到系统全局程序集缓存 (GAC)。 如果你想要将部署到 Web 应用程序 (Bin) 文件夹的程序集，请改为选择该选项。 有关详细信息，请参阅[在 SharePoint Foundation 中部署 Web 部件](http://go.microsoft.com/fwlink/?LinkId=177509)。

11. 在中**安全控件**框中，选择**单击此处可添加新项**按钮。

12. 下表中所输入的属性的值。

    |属性名|“值”|
    |-------------------|-----------|
    |命名空间|完全限定命名空间进行控制，如**BdcModelProject1.VisualWebPart1**。|
    |类型名称|Button1|
    |程序集名称|强的程序集名称，例如：Microsoft.Office.SharePoint.ClientExtensions，Version = 14.0.0.0，区域性 = 中性，PublicKeyToken = 71e9bce111e9429c。|
    |安全|清除**安全**复选框。|
    |安全应对脚本|将保留**安全应对脚本**复选框为空。|

    > [!NOTE]
    > **程序集名称**通过添加的程序集的值**高级**选项卡**包设计器**不能将一个令牌，它必须是强名称程序集。 有关详细信息，请参阅[创建和使用具有强名称的程序集](http://go.microsoft.com/fwlink/?LinkId=177513)。

13. 选择**选项卡**密钥，以创建另一个安全控件项。

14. 选择**单击此处可添加新项**按钮再次。

15. 下表中所输入的属性的值。

    |属性名|“值”|
    |-------------------|-----------|
    |命名空间|完全限定命名空间进行控制，如**BdcModelProject1.VisualWebPart1**。|
    |类型名称|TextBox1|
    |程序集名称|强的程序集名称，例如：Microsoft.Office.SharePoint.ClientExtensions，Version = 14.0.0.0，区域性 = 中性，PublicKeyToken = 71e9bce111e9429c。|
    |安全|选择**安全**复选框。|
    |安全应对脚本|选择**安全应对脚本**复选框。|

16. 选择**选项卡**键，，然后选择**确定**按钮以关闭对话框。

## <a name="see-also"></a>请参阅
- [提供在项目项中的打包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
