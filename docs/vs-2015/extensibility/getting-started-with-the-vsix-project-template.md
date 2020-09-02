---
title: 与 VSIX 项目模板入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
caps.latest.revision: 26
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cc3f461c9e7dbdea1fd8481594292a0a247d2173
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204302"
---
# <a name="getting-started-with-the-vsix-project-template"></a>VSIX 项目模板入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用 VSIX 项目模板来创建扩展或打包现有扩展以进行部署。 VSIX 项目模板同时具有 Visual Basic 和 Visual c # 版本，并作为 Visual Studio SDK 的一部分安装。  
  
 VSIX 项目模板只包含一个 source.extension.vsixmanifest 文件，其中包含有关扩展和所提供的资产的信息。  
  
 若要查找 VSIX 项目模板，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。  
  
## <a name="deploying-a-custom-project-template-using-the-vsix-project-template"></a>使用 VSIX 项目模板部署自定义项目模板  
 以下步骤演示如何使用 VSIX 项目来打包可与其他开发人员共享或上传到 Visual Studio 库的项目模板。  
  
1. 创建项目模板。  
  
    1. 打开要从中创建模板的项目。 此项目可以是任何项目类型。  
  
    2. 在“文件”**** 菜单上，单击“导出模板”****。 完成向导的步骤。  
  
         在%USERPROFILE%\My Documents\Visual Studio \My 导出的模板中创建一个 .zip 文件 *\<version>* \\ 。  
  
2. 创建一个空 VSIX 项目。  
  
     在“文件”菜单上，单击“新建”，然后单击“项目”。 选择 " **Visual Basic** " 或 " **Visual c #**"。 在选定节点下，选择 " **扩展性**"，然后选择 " **VSIX 项目**"。  
  
3. 将 .zip 文件添加到项目。 将其 " **复制到输出目录** " 属性设置为 `Copy Always` 。  
  
4. 在 **解决方案资源管理器**中，双击该 `source.extension.vsixmanifest` 文件以在 **VSIX 清单设计器**中将其打开，然后进行以下更改：  
  
    - 将 " **产品名称** " 字段设置为 **"我的项目模板**"。  
  
    - 将 " **产品 ID** " 字段设置为 **MyProjectTemplate-1**。  
  
    - 将 **Author** 字段设置为 **Fabrikam**。  
  
    - 将 " **说明** " 字段设置为 **"我的项目模板**"。  
  
    - 在 " **资产** " 部分中，添加 **VisualStudio. ProjectTemplate** 类型，并将其路径设置为 .zip 文件的名称。  
  
5. 保存并关闭 source.extension.vsixmanifest 文件。  
  
6. 生成项目。  
  
7. 在输出目录中，双击 .vsix 文件。  
  
8. 此时将显示 " **VSIX 安装程序** " 消息框。 按照说明安装扩展。  
  
9. 关闭 Visual Studio，然后重新打开它。  
  
10. 在 "**工具**" 菜单上选择 "**扩展和更新**" () 并选择 "**模板**" 类别。 其中一个可用扩展应为 **"我的项目模板**"。  
  
11. 新的项目模板将显示在 " **新建项目** " 对话框中，与原始项目模板位于同一位置。 例如，如果从 Visual Basic 控制台应用程序创建了名为 **Vb 控制台** 的模板，则 **VB 控制台** 将显示在与 Visual Basic **控制台应用程序** 模板相同的窗格中。  
  
#### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>在 "新建项目" 对话框中指定模板的位置  
  
1. 模板文件夹位于 *Visual Studio 安装路径*\Common7\IDE\ProjectTemplates 和 *Visual studio 安装路径*\Common7\IDE\ItemTemplates 目录中。 "新建项目" 对话框中的顶级部分的名称与模板文件夹的名称不完全匹配。 如果二者不同，请使用模板文件夹的名称。  
  
     将 .vsix 文件扩展名更改为 .zip，然后打开该文件。  
  
2. 创建与 "新建项目" 对话框中的部分名称相同的新文件夹，模板应出现在该对话框中。  
  
3. 如果模板要出现在子节中，请创建一个具有相同名称的子文件夹。  
  
4. 将模板 .zip 文件移到新文件夹中。  
  
5. 将 .zip 扩展名更改为 .vsix。  
  
6. 打开 VSIX 清单。  
  
7. 在 VSIX 清单中，更新模板的 **资产** 路径，使其指向包含模板文件的目录树的根。 例如，如果模板位于 \CSharp\Windows 中，则该引用应指向 \CSharp。
