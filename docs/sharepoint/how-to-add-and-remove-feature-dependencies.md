---
title: 如何：添加和移除功能依赖项 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c318a7dc4672a10e993d0149ec77e7f94679d465
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014776"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>如何：添加和移除功能依赖项
  SharePoint 功能可能取决于功能或数据的其他功能。 在这些情况下，你可以将这些其他功能标记为功能的依赖项。 这样一来，SharePoint server 确保在激活功能之前激活依赖功能。

## <a name="add-dependencies"></a>添加依赖项
 可以将解决方案中的其他功能添加为依赖项。 这样，你可以确保在安装功能之前安装并激活必需的功能。

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>在解决方案中添加对功能的依赖项

1. 打开功能设计器，展开 "**功能激活依赖项**" 节点，然后选择 "**添加**" 按钮。

2. 在 "**添加功能激活依赖项**" 对话框中，选择 "在**解决方案中添加功能的依赖项"** 选项按钮，选择要添加为依赖项的功能的标题，然后选择 "**添加**" 按钮。

     可以通过在选择**Ctrl**键的同时选择多个标题来添加多个功能。

## <a name="addi-custom-dependencies"></a>Addi 自定义依赖项
 你可以将已在 SharePoint 服务器上部署的功能添加为依赖项。 这样一来，SharePoint 激活过程将进行检查以确保在安装功能之前激活所有依赖功能。

#### <a name="to-add-a-dependency-by-the-feature-id"></a>按功能 ID 添加依赖项

1. 打开功能设计器，展开 "**功能激活依赖项**" 节点，然后选择 "**添加**" 按钮。

2. 在 "**添加功能激活依赖项**" 对话框中，选择 "**添加自定义依赖项**" 选项按钮。

3. 在 "**功能 ID** " 文本框中，输入要标记为激活依赖项的功能的 GUID，然后选择 "**添加**" 按钮。

## <a name="edit-custom-dependencies"></a>编辑自定义依赖项
 你可以编辑你先前添加的自定义依赖项。 但是，您的解决方案中的依赖功能只能被删除，而不能编辑。

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>更改对解决方案中某个功能的依赖关系

1. 打开功能设计器，然后展开 "**功能激活依赖项**" 节点。

2. 选择要编辑的功能的名称，然后选择 "**编辑**" 按钮。

3. 在 "**编辑自定义功能激活依赖项**" 对话框中，更改 "标题"、"功能 ID" 或 "说明"，然后选择 "**提交**" 按钮。

## <a name="remove-dependencies"></a>删除依赖项

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>删除解决方案中某个功能的依赖项

1. 在功能设计器中，展开 "**功能激活依赖项**" 节点，选择要删除的功能的名称，然后选择 "**删除**" 按钮。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：在 SharePoint 功能中添加和移除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
