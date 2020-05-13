---
title: VSIX 项目模板 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 74791a77ee1c720fb60876a1efa6bd58fa94f68b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697925"
---
# <a name="vsix-project-template"></a>VSIX 项目模板

您可以使用 VSIX 项目模板在 VSIX 项目中包装一个或多个 Visual Studio 扩展，然后在[可视化工作室应用商店](https://marketplace.visualstudio.com/)网站上发布包。

 VSIX 部署支持 VS 包、程序集、MEF 组件、项目模板、项目模板、工具箱控件和自定义扩展类型。

> [!NOTE]
> 要使用 VSIX 项目，必须安装可视化工作室 SDK。 有关可视化工作室 SDK 的详细信息，请参阅[可视化工作室 SDK](../extensibility/visual-studio-sdk.md)。

## <a name="where-to-find-the-vsix-project-template"></a>在哪里可以找到 VSIX 项目模板

通过搜索"vsix"，"**新项目**"对话框中提供了 VSIX 项目模板。  有 C# 和可视化基本版本。

> [!TIP]
> 应确保在 **"新项目"** 对话框顶部的下拉列表框中指定 .NET Framework 4.5 或更高版本。

## <a name="uses-of-the-vsix-project-template"></a>VSIX 项目模板的使用

VSIX 项目模板有两个主要用途：

- 部署项目模板、项目模板和扩展。

- 将多个扩展的输出包装到一个部署包中。

## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>在空 VSIX 项目中打包扩展

通过将现有扩展或尚未具有 VSIX 支持的扩展打包在空 VSIX 项目中，可以打包现有扩展或尚未具有 VSIX 支持的扩展。 要包装的扩展必须为[VSIX 架构](../extensibility/vsix-extension-schema-2-0-reference.md)支持的类型。

### <a name="to-package-an-extension-by-using-a-vsix-project"></a>使用 VSIX 项目打包扩展

1. 生成构成扩展的项目。

2. 使用 VSIX 项目模板创建**VSIX 项目**。

    *源.扩展.vsixmanifest*在**清单设计器**中打开。

3. 在"**资产**"选项卡上，选择"**新建"** 按钮。

    将显示"**添加新资产**"对话框。

4. 在 **"类型"** 列表中，选择要添加的扩展类型。

5. 要添加当前解决方案中包含的扩展或内容元素（例如，项模板或已编译的程序集），执行以下步骤：

   1. 在 **"源"** 列表中，选择**当前解决方案中的项目**。

   2. 在 **"项目"** 列表中，选择扩展名的名称。

   3. **在此文件夹框中的"嵌入"** 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定**"按钮。

6. 要添加当前解决方案中未包含的扩展或内容元素，执行以下步骤：

   1. 在 **"源"** 列表框中，选择**文件系统上的"文件**"。

   2. 在 **"路径"** 字段中，输入已编译或压缩扩展文件的完整路径，或使用 **"浏览"** 按钮浏览到该文件。

   3. **在此文件夹框中的"嵌入"** 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定**"按钮。

7. 如果希望包包含其他扩展，请以相同的方式添加它们。

8. 生成解决方案。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]生成包含 VSIX 清单文件、[Content_Types]*.xml*文件以及添加到项目的所有扩展资源的所有 *.vsix*文件。

## <a name="see-also"></a>请参阅

- [VSIX 扩展架构 2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)
- [查找和使用可视化工作室扩展](../ide/finding-and-using-visual-studio-extensions.md)
