---
title: 准备 Windows Installer 部署的扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 76d7f879fade99914bf3f56ade0ec1270e14f4c7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65694597"
---
# <a name="preparing-extensions-for-windows-installer-deployment"></a>准备 Windows Installer 部署的扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

不能使用 Windows Installer 包 (MSI) 来部署 VSIX 包。 不过，您可以提取用于 MSI 部署的 VSIX 包的内容。 本文档演示如何准备一个项目，该项目的默认输出是一个要包含在安装项目中的 VSIX 包。  
  
## <a name="preparing-an-extension-project-for-windows-installer-deployment"></a>为 Windows Installer 部署准备扩展项目  
 在添加到安装项目之前，请在新的扩展项目中执行这些步骤。  
  
#### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>为 Windows Installer 部署准备扩展项目  
  
1. 创建包含 VSIX 清单的 VSPackage、MEF 组件、编辑器修饰或其他扩展性项目类型。  
  
2. 在代码编辑器中打开 VSIX 清单。  
  
3. 将 VSIX 清单的 InstalledByMsi 元素设置为 `true` 。 有关 VSIX 清单的详细信息，请参阅 [Vsix 扩展架构2.0 引用](../extensibility/vsix-extension-schema-2-0-reference.md)。  
  
     这会阻止 VSIX 安装程序尝试安装该组件。  
  
4. 右键单击 " **解决方案资源管理器** 中的项目，然后单击" **属性**"。  
  
5. 选择 " **VSIX** " 选项卡。  
  
6. 选中标签 " **将 VSIX 内容复制到以下位置** " 框，然后键入安装项目将选取文件的路径。  
  
## <a name="extracting-files-from-an-existing-vsix-package"></a>从现有 VSIX 包提取文件  
 如果没有源文件，请执行以下步骤将现有 VSIX 包的内容添加到安装项目。  
  
#### <a name="to-extract-files-from-an-existing-vsix-package"></a>从现有 VSIX 包提取文件  
  
1. 重命名。包含从 *文件名*.vsix 到 *filename*.ZIP 的扩展的 VSIX 文件。  
  
2. 将 .zip 文件的内容复制到目录中。  
  
3. 从目录中删除 [Content_types] .xml 文件。  
  
4. 如前面的过程所示，编辑 VSIX 清单。  
  
5. 将剩余文件添加到安装项目。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 安装程序部署](https://msdn.microsoft.com/121be21b-b916-43e2-8f10-8b080516d2a0)   
 [演练：创建自定义操作](https://msdn.microsoft.com/4bd4b63a-2b91-431e-839c-5752443f0eaf)
