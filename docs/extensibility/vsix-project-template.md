---
title: VSIX 项目模板 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc2600a6c72e13ba7d894dab84f0b8a171d5a43e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322825"
---
# <a name="vsix-project-template"></a>VSIX 项目模板

可以使用 VSIX 项目模板将一个或多个 Visual Studio 扩展包装在 VSIX 项目，然后将包发布上[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web 站点。

 VSIX 部署支持 Vspackage、 程序集、 MEF 组件、 项目模板、 项模板，工具箱控件和自定义扩展插件类型。

> [!NOTE]
> 若要使用 VSIX 项目，必须安装 Visual Studio SDK。 有关 Visual Studio SDK 的详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="where-to-find-the-vsix-project-template"></a>在哪里可以找到 VSIX 项目模板

VSIX 项目模板现已推出**新的项目**通过搜索"vsix"对话框。  没有同时C#和 Visual Basic 版本。

> [!TIP]
> 请确保该.NET Framework 4.5 或更高版本顶部的下拉列表框中指定**新的项目**对话框。

## <a name="uses-of-the-vsix-project-template"></a>VSIX 项目模板的用途

VSIX 项目模板具有两个主要用途：

- 若要部署的项目模板、 项模板和扩展。

- 若要将多个扩展的输出包装到一个部署包。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>打包在一个空的 VSIX 项目中的扩展

您可以打包现有扩展插件或不具有支持，通过将其包装在一个空的 VSIX 项目中的 VSIX 扩展。 要包装的扩展必须支持的类型的[VSIX 架构](../extensibility/vsix-extension-schema-2-0-reference.md)。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>若要将扩展打包使用 VSIX 项目

1. 生成构成了您的扩展插件项目。

2. 使用创建 VSIX 项目**VSIX 项目**模板。

    *Source.extension.vsixmanifest*中打开**清单设计器**。

3. 上**资产**选项卡上，选择**新建**按钮。

    **添加新资产**对话框随即出现。

4. 在中**类型**列表中，选择要添加的扩展类型。

5. 若要添加包含在当前解决方案 （例如，项模板或已编译的程序集） 的扩展插件或内容元素，请执行以下步骤：

   1. 在中**源**列表中，选择**当前解决方案中的项目**。

   2. 在中**项目**列表中，选择扩展插件的名称。

   3. 在中**在此文件夹中的嵌入**框中，输入在其中以嵌入资产，然后选择的文件夹的名称**确定**按钮。

6. 若要添加的扩展或不包括在当前解决方案的内容元素，请执行以下步骤：

   1. 在中**源**列表框中，选择**在文件系统上的文件**。

   2. 在中**路径**字段中，已编译或压缩扩展文件中，输入完整路径或使用**浏览**按钮以浏览到该文件。

   3. 在中**在此文件夹中的嵌入**框中，输入在其中以嵌入资产，然后选择的文件夹的名称**确定**按钮。

7. 如果你想要包括的其他扩展包，则将它们添加相同的方式。

8. 生成解决方案。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成 *.vsix*文件，其中包含 VSIX 清单文件，[Content_Types] *.xml*文件，以及所有添加到项目中的扩展资产。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构 2.0 参考](../extensibility/vsix-extension-schema-2-0-reference.md)
- [查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)