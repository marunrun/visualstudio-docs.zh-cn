---
title: 如何：添加和删除功能依赖关系 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 9373ed07ec49bd41dad343dc447b4b2026793492
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62966999"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>如何：添加和删除功能依赖关系
  SharePoint 功能可能依赖的功能或数据的其他功能。 在这些情况下，可以将这些其他功能为您的功能标记为依赖项。 这样一来，SharePoint 服务器会确保你的功能被激活之前激活相关功能。

## <a name="add-dependencies"></a>添加依赖项
 为依赖项，可以在解决方案中添加其他功能。 这样一来，可以确保安装并激活，然后安装您的功能所需的功能。

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>若要添加该解决方案中的功能的依赖项

1. 打开功能设计器中，依次展开**功能激活依赖项**节点，然后选择**添加**按钮。

2. 在中**添加功能激活依赖项**对话框框中，选择**添加该解决方案中的功能的依赖项**选项按钮，选择想要添加为一个依赖项，该功能的标题，然后选择**添加**按钮。

     可以通过选择同时选择多个标题来添加多个功能**Ctrl**密钥。

## <a name="addi-custom-dependencies"></a>逐个自定义依赖项
 作为依赖项，可以在 SharePoint 服务器上添加已部署的功能。 这样一来，SharePoint 激活过程会检查以确保安装你的功能之前，激活所有依存功能。

#### <a name="to-add-a-dependency-by-the-feature-id"></a>若要添加的功能 ID 的依赖项

1. 打开功能设计器中，依次展开**功能激活依赖项**节点，然后选择**添加**按钮。

2. 在中**添加功能激活依赖项**对话框框中，选择**添加自定义依赖项**选项按钮。

3. 在中**功能 ID**文字框中，输入你想要将标记为激活依赖项，然后选择功能的 GUID**添加**按钮。

## <a name="edit-custom-dependencies"></a>编辑自定义依赖项
 您可以编辑以前添加的自定义依赖项。 但是，相关功能在解决方案可以仅删除，不能编辑。

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>若要更改解决方案中的功能上的依赖项

1. 打开功能设计器中，，然后展开**功能激活依赖项**节点。

2. 选择你想要编辑，然后选择功能名称**编辑**按钮。

3. 在中**编辑自定义功能激活依赖项**对话框中，更改的标题、 功能 ID 或描述，然后选择**提交**按钮。

## <a name="remove-dependencies"></a>删除依赖项

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>若要在解决方案中删除上一项功能的依赖项

1. 在功能设计器中，展开**功能激活依赖项**节点，选择你想要删除，然后选择功能名称**删除**按钮。

## <a name="see-also"></a>请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：添加和删除项 SharePoint 功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
