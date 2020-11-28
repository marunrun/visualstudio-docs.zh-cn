---
title: 如何：使用模块包括文件 |Microsoft Docs
description: 了解如何通过使用模块来包含文件，该模块可让你将文件（如 ASPX 母版页、文本文件或图像）部署到 SharePoint。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 381cb529db3f4116a9c42041c26e0e1e242073df
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305417"
---
# <a name="how-to-include-files-by-using-a-module"></a>如何：使用模块包括文件
  *模块* (不会与模块混淆 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) 为容器，使你能够将 ASPX 母版页、文本文件或图像等文件部署到 SharePoint。

 您可以选择将文件部署到文档库中，也可以选择将文件部署为常规文件 (例如) 文档库之外的 .aspx。 若要将文件添加到文档库，请将指定 `Type="GhostableInLibrary"` 为 **file** 元素中的属性。 此设置指示 SharePoint 在将文件添加到库时，创建一个用于文件的列表项。 若要在文档库外部部署文件，请指定 `Type="Ghostable"` 或仅省略 **Type** 特性。

## <a name="add-a-module-to-a-sharepoint-solution"></a>向 SharePoint 解决方案添加模块

#### <a name="to-add-a-module"></a>添加模块

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **解决方案资源管理器** 中，选择 "项目" 节点，然后在菜单栏上选择 "**项目**" "  >  **添加新项**"。

     此时将打开“添加新项”  对话框。

3. 在 SharePoint 模板列表中，选择 " **模块** " 模板，然后选择 " **添加** " 按钮。

     此步骤将在项目中创建名为 Module1 的节点。

4. 在 Module1 下，删除 *Sample.txt* 文件。

     出于举例目的，Sample.txt 包含在所有新的模块中，因此不需要。  (请注意，删除文件还会从模块的 *Elements.xml* 文件中删除其条目。 ) 

5. 如果希望将文件部署到 SharePoint 中的特定文件夹结构，请 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 选择 "module1" 节点，然后在菜单栏上选择 " **项目**"、" **新建文件夹**"，以在 Module1 下创建这些文件夹。

6. 选择要在其中添加文件的文件夹，然后在菜单栏上选择 " **项目**"、" **添加现有项**"。

7. 选择一个或多个要部署到 SharePoint 的文件，然后选择 " **添加** " 按钮。

     向项目中添加文件时，会自动将一个项添加到该模块的 Elements.xml 文件中。 部署项目时，文件将复制到 SharePoint server （相对于项目的根目录），该目录由 **文件** 元素的 **Url** 属性指定，如 `Url="Module1/New Folder/SomeFile.doc` 。 如果要更改文件的部署位置，请将其移动到 **解决方案资源管理器** 中的其他文件夹或更改其 **Url** 设置。

8. 对于想要在文档库中显示的任何文件，请将该 `Type="GhostableInLibrary"` 属性追加到 *Elements.xml* 中的条目。 例如，

    ```xml
    <File Path="Module1\Some Folder\SomePage.aspx" Url="Module1/Some Folder/SomePage.aspx" Type="GhostableInLibrary" />
    ```

9. 部署该项目。

     文件复制到 SharePoint 中的指定位置。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
