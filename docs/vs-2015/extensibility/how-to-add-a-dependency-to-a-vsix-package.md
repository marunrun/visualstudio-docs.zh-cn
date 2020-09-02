---
title: 如何：向 VSIX 包添加依赖项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- package reference
- package assembly
- package dll
- vsix reference
ms.assetid: 8f20177b-dab9-43a3-b959-81a591b451d6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 997c0df133b72d69dfb4e69de53a1b77e1a0965c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697506"
---
# <a name="how-to-add-a-dependency-to-a-vsix-package"></a>如何：将依赖项添加到 VSIX 包
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以设置一个 VSIX 包部署，用于安装目标计算机上尚不存在的任何依赖项。 若要实现此目的，请将 VSIX 依赖项包含到 source.extension.vsixmanifest 文件。  
  
#### <a name="to-add-a-dependency"></a>添加依赖项  
  
1. 在 " **设计** " 视图中打开 source.extension.vsixmanifest 文件。 单击 " **依赖项** " 选项卡，然后单击 " **新建**"。  
  
2. 添加已安装的扩展：在 " **添加新的依赖项** " 对话框中，选择 " **已安装的扩展** "，然后对于 " **名称**"，请在列表中选择一个扩展。  
  
3. 添加另一个未安装的 VSIX：：在 " **添加新的依赖项** " 对话框中，选择 "文件 **系统** "，然后使用 " **浏览** " 按钮选择 VSIX。  
  
## <a name="see-also"></a>另请参阅  
 [VSIX 扩展架构1.0 引用](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)   
 [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)   
 [准备 Windows Installer 部署的扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)
