---
title: 如何：添加和移除映射的文件夹 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.MappedFolder
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, mapped folders
- mapped folders [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d5d1acc40b23c979a5746c50be50a584d11112b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966908"
---
# <a name="how-to-add-and-remove-mapped-folders"></a>如何： 添加和移除映射的文件夹
  一些常用的文件夹在 SharePoint 中，如图像和布局，深度嵌套的文件层次结构中。 可以将这些文件夹映射到 SharePoint 项目来更轻松地访问它们。 映射的文件夹是 SharePoint 项目中的 SharePoint 服务器安装文件的物理位置相对应的文件夹。

 在部署 SharePoint 应用程序时，映射的文件夹和所有子文件夹由解决方案包 (.wsp) 复制到服务器上的内容的正在运行 SharePoint 的 SharePoint 文件夹树中的指定位置。 此位置由**部署位置**为映射文件夹设置的属性。 映射文件夹中的任何子文件夹是相对于**部署位置**的映射文件夹。 请注意，**部署位置**属性，不是映射文件夹的名称确定项的部署位置。
使用命令在菜单栏或快捷菜单上的项目，可以将映射的文件夹添加到项目。 可以使用**添加 SharePoint"Images"映射文件夹**并**添加 SharePoint"布局"文件夹**命令来添加这些映射最常使用的文件夹。 您可以通过使用将任何其他可用的 SharePoint 文件夹映射到你的项目**添加 SharePoint 映射文件夹**命令的快捷菜单上，然后指定文件夹中的**添加 SharePoint 映射文件夹**对话框。

## <a name="add-mapped-folders-to-a-project"></a>将映射的文件夹添加到项目
 以下过程介绍如何将两个映射的文件夹添加到可视化 web 部件项目。 若要开始，你创建可视化 web 部件项目。

#### <a name="to-add-mapped-folders-to-a-project"></a>若要将映射的文件夹添加到项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在中**新的项目**对话框框中，展开**Visual Basic**或**Visual C#** 节点中，展开**Office/SharePoint**节点，然后选择**SharePoint 解决方案**节点。

3. 在项目模板列表中，选择**SharePoint 2013 可视 Web 部件**模板。

4. 在中**名称**框中，输入**TestProject1**，然后选择**确定**按钮。

5. 在中**SharePoint 自定义向导**，选择**完成**按钮，保留默认设置。

6. 在中**解决方案资源管理器**，选择项目节点，然后，在菜单栏上选择**项目** > **添加 SharePoint"Images"映射文件夹**。

     名为的文件夹**映像**将出现在你的项目，并包含名为 TestProject1 的子文件夹。 此映射的文件夹将包含可视 web 部件项目的映像。

7. 在中**解决方案资源管理器**，选择项目节点，然后，在菜单栏上选择**项目** > **添加 SharePoint 映射文件夹**显示**添加 SharePoint 映射文件夹**对话框。

8. 在可用于映射的文件夹树视图中，选择**资源**文件夹，然后选择**确定**按钮。

     名为的文件夹**资源**将出现在你的项目。 此文件夹可以用于存储字符串资源文件等项。 子文件夹也可用于组织的映射文件夹的内容，但它们不会自动创建时使用添加的映射的文件夹**添加 SharePoint 映射文件夹**命令。 若要添加子文件夹，选择**资源**文件夹，然后在菜单栏上选择**项目** > **新文件夹**。

## <a name="change-the-deployment-location-of-a-mapped-folder"></a>更改的映射文件夹的部署位置
 默认情况下映射的文件夹添加到特定位置相对于 SharePoint 根安装路径，该令牌\<SharePointRoot > 表示。 但是，可以通过更改来更改此位置**部署位置**的映射文件夹的属性。 每个映射的文件夹都具有其自己**部署位置**属性。

#### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>若要更改的映射文件夹的部署位置

1. 在前面创建的项目，选择映射的文件夹。

2. 在中**属性**窗口中，选择省略号 (![ASP.NET 移动设计器椭圆](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器椭圆")) 按钮**部署位置**属性。

3. 在中**添加 SharePoint 映射文件夹**对话框中，浏览到要点的映射的文件夹的文件夹。

4. 选择节点，然后选择**确定**按钮。

## <a name="rename-or-remove-mapped-folders"></a>重命名或移除映射的文件夹

#### <a name="to-rename-or-remove-a-mapped-folder"></a>若要重命名或删除的映射的文件夹

1. 在前面创建的项目，选择映射的文件夹。

2. 若要重命名映射的文件夹，打开其快捷菜单，选择**重命名**，输入新名称，然后选择 Enter 键。

     作为替代方法，你可以选择你想要重命名，打开映射的文件夹**属性**窗口中，然后将的值设置**文件夹名称**属性设置为新名称。

3. 若要从项目中删除的映射的文件夹，打开其快捷菜单，选择**删除**，然后选择**确定**以确认删除对话框中的按钮。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
