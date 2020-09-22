---
title: VSIX 项目模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2386f1be805f6347fc32fba4ee8bfe57c8602329
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840735"
---
# <a name="vsix-project-template"></a>VSIX 项目模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用 "VSIX 项目" 模板来包装 VSIX 项目中的一个或多个 Visual Studio 扩展，然后在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站上发布包。  
  
 VSIX 部署支持 Vspackage、程序集、MEF 组件、项目模板、项模板、工具箱控件和自定义扩展类型。  
  
> [!NOTE]
> 若要使用 VSIX 项目，必须安装 Visual Studio SDK。 有关 Visual Studio SDK 的详细信息，请参阅 [Visual STUDIO sdk](../extensibility/visual-studio-sdk.md)。  
  
## <a name="where-to-find-the-vsix-project-template"></a>在何处查找 VSIX 项目模板  
 " **新建项目** " 对话框中提供了 "VSIX 项目" 模板。 展开 " **Visual Basic** " 节点或 " **Visual c #** " 节点，然后选择 " **扩展性**"。  
  
> [!TIP]
> 应确保在 " **新建项目** " 对话框顶部的下拉列表中指定 .NET Framework 4.5 或更高版本。  
  
## <a name="uses-of-the-vsix-project-template"></a>使用 VSIX 项目模板  
 VSIX 项目模板有两个主要用途：  
  
- 部署项目模板、项模板以及尚未提供 VSIX 支持的其他扩展。  
  
- 将多个扩展的输出包装在一个部署包中。  
  
  您无需使用 VSIX 项目模板来部署 Vspackage 或其他类型的扩展，这些扩展已具有 VSIX 支持。  
  
## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>在空 VSIX 项目中打包扩展  
 可以通过将现有的扩展包装到空的 VSIX 项目中来打包现有扩展或尚未提供 VSIX 支持的扩展。 要包装的扩展必须是 [VSIX 架构](../extensibility/vsix-extension-schema-2-0-reference.md)支持的类型。  
  
#### <a name="to-package-an-extension-by-using-a-vsix-project"></a>使用 VSIX 项目打包扩展  
  
1. 生成组成扩展的项目。  
  
2. 使用 **Vsix 项目** 模板创建一个 vsix 项目。  
  
     Source.extension.vsixmanifest 在 **清单设计器**中打开。  
  
3. 在 " **资产** " 选项卡上，选择 " **新建** " 按钮。  
  
     此时将显示 " **添加新资产** " 对话框。  
  
4. 在 " **类型** " 列表中，选择要添加的扩展的类型。  
  
5. 若要添加当前解决方案中包含的 extension 或 content 元素 (例如，项模板或编译的程序集) ，请执行以下步骤：  
  
    1. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。  
  
    2. 在 " **项目** " 列表中，选择扩展插件的名称。  
  
    3. 在 " **嵌入此文件夹** " 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定"** 按钮。  
  
6. 若要添加当前解决方案中未包含的 extension 或 content 元素，请执行以下步骤：  
  
    1. 在 " **源** " 列表框中，选择 **文件系统上的文件**。  
  
    2. 在 " **路径** " 字段中，输入编译或压缩的扩展文件的完整路径，或者使用 " **浏览** " 按钮浏览到该文件。  
  
    3. 在 " **嵌入此文件夹** " 框中，输入要嵌入资产的文件夹的名称，然后选择 **"确定"** 按钮。  
  
7. 如果希望包包含其他扩展，请以相同方式添加它们。  
  
8. 生成解决方案。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 生成一个 .vsix 文件，其中包含一个 VSIX 清单文件、一个 [Content_Types] .xml 文件和您添加到项目中的所有扩展资产。  
  
## <a name="see-also"></a>另请参阅  
 [VSIX 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)   
 [查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)
