---
title: 如何：添加和删除其他程序集 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.RAD.CustomAssembly
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fa25413a40c9b2333acbaba96d55008dbcebfd39
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967025"
---
# <a name="how-to-add-and-remove-additional-assemblies"></a>如何：添加和删除其他程序集
  如果 SharePoint 包依赖于其他程序集的功能或数据，则可以将程序集添加到解决方案包 (.wsp)。 这样一来，在 SharePoint 服务器可确保自定义程序集随包一起安装。

 您还可以添加和更改的安全控件和类资源文件与程序集关联。

## <a name="add-additional-assemblies-safe-controls-and-class-resources"></a>添加其他程序集、 安全控件和类资源
 您可以添加到 SharePoint 解决方案包的其他程序集。 沙盒解决方案中的其他程序集部署到全局程序集缓存中，但沙盒解决方案中的 SharePoint 项目项添加到内容数据库。 此外可以对这些其他程序集添加安全控件和类资源。 有关安全控件的详细信息，请参阅[提供打包和部署项目项中的信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)或"创建 SafeControl 条目"中[SharePoint Foundation 中部署 Web 部件](http://go.microsoft.com/fwlink/?LinkId=245505)。

#### <a name="to-add-an-existing-assembly"></a>若要添加的现有程序集

1. 打开**包设计器**。 有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择**高级**选项卡。

3. 选择**外**按钮，，然后选择**添加现有程序集**从列表中。

     **添加现有程序集**对话框随即出现。

4. 选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆"))，然后选择你想要添加的程序集。 我们建议使用可移植性用途的所选程序集的相对路径。

5. 有关**部署目标**，选择**GlobalAssemblyCache**选项按钮以将程序集部署到全局程序集缓存中，或选择**WebApplication**选项若要将程序集部署到运行 SharePoint 服务器上的 web 应用程序文件夹的按钮。

#### <a name="to-add-an-assembly-from-project-output"></a>若要从项目输出添加程序集

1. 打开**包设计器**。

     有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择**高级**选项卡。

3. 选择**外**按钮，，然后选择**从项目输出添加程序集**从列表中。

     **从项目输出添加程序集**对话框随即出现。

4. 在中**源项目**列表，并选择你想要添加的源项目。

5. 有关**部署目标**，选择**GlobalAssemblyCache**选项按钮以将程序集部署到全局程序集缓存中，或选择**WebApplication**选项若要将程序集部署到运行 SharePoint 服务器上的 web 应用程序文件夹的按钮。

#### <a name="to-add-a-safe-control"></a>若要添加安全控件

1. 打开**编辑现有程序集**对话框。 若要完成此操作，打开包设计器中，选择**高级**选项卡上，选择一个程序集，然后选择**编辑**按钮。

2. 在中**安全控件**窗格中，选择**单击此处可添加新项**按钮。

3. 在中**程序集名称**列中，输入程序集的名称。

4. 在中**Namespace**列中，输入安全控件的命名空间的名称。

5. 在中**类型名称**列中，输入类型的名称。

#### <a name="to-add-a-class-resource"></a>若要添加的类资源

1. 打开**编辑现有程序集**对话框。 若要完成此操作，打开包设计器中，选择**高级**选项卡上，选择一个程序集，然后选择**编辑**按钮。

2. 在中**类的资源**窗格中，选择**单击此处可添加新项**按钮。

3. 在中**文件名**列中，选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆"))，并选择你想要添加的类资源。

## <a name="delete-custom-assemblies"></a>删除自定义程序集
 您可以从 SharePoint 包，删除程序集或从现有程序集删除安全控件和类资源。

#### <a name="to-delete-an-existing-assembly"></a>若要删除的现有程序集

1. 打开**包设计器**。 有关详细信息，请参阅[如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)。

2. 选择**高级**选项卡。

3. 在中**其他程序集**窗格中，选择你想要删除的自定义程序集。

4. 选择**删除**按钮。

#### <a name="to-delete-a-safe-control-for-an-assembly"></a>若要删除的程序集的安全控件

1. 打开**编辑现有程序集**对话框。 若要完成此操作，打开包设计器中，选择**高级**选项卡上，选择一个程序集，然后选择**编辑**按钮。

2. 选择你想要删除的安全控件。

3. 选择 Delete 键。

#### <a name="to-delete-a-class-resource-for-an-assembly"></a>若要删除的程序集的类资源

1. 打开**编辑现有程序集**对话框。 若要完成此操作，打开包设计器中，选择**高级**选项卡上，选择一个程序集，然后选择**编辑**按钮。

2. 选择你想要删除的类资源。

3. 选择 Delete 键。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：添加和删除项 SharePoint 功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
