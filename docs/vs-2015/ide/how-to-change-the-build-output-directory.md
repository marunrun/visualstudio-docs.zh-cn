---
title: 如何：更改生成输出目录 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- output directory, changing
ms.assetid: a8333c89-afb2-4b1d-b2e2-9146da852402
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 968a9a2dc87063baec075e69e10fed96ba1ff3d5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65680584"
---
# <a name="how-to-change-the-build-output-directory"></a>如何：更改生成输出目录
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以按项目生成的配置（调试、发布或两者）指定输出的位置。  
  
> [!NOTE]
> 如果你具有“安装”  项目，请参阅本文末尾处的注释。  
  
## <a name="changing-the-build-output-directory"></a>更改生成输出目录  
  
#### <a name="to-change-the-build-output-directory"></a>若要更改生成输出目录  
  
1. 在菜单栏上，选择 **“项目”**、 *AppName* **“属性”**。 还可以在 **“解决方案资源管理器”** 中右键单击项目节点并选择 **“属性”**。  
  
2. 如果你有 Visual Basic 项目，请选择 **“编译”** 选项卡。如果你有 Visual C# 项目，请选择 **“编译”** 选项卡。如果你具有 C++ 项目或 JavaScript 项目，请选择 **“常规”** 选项卡。  
  
3. 在顶部的配置下拉列表中，选择你想要更改其输出文件位置的配置（调试、发布或全部）。  
  
     查找输出路径条目（Visual Basic 中的 **“生成输出路径”** ，Visual C++中的 **“输出目录”** ，JavaScript 和 C# 中的 **“输出路径”** ）。 指定一个相对于项目目录的新的生成输出目录。  
  
> [!NOTE]
> 在“安装”项目中，“输出文件名称”  框仅更改 Setup.exe 文件的位置，而不更改项目文件的位置。 有关详细信息，请参阅 **生成、配置属性、“部署项目属性”对话框**。  
  
## <a name="see-also"></a>请参阅  
 [生成页、项目设计器 (C#)](../ide/reference/build-page-project-designer-csharp.md)   
 [常规属性页（项目）](https://msdn.microsoft.com/library/593b383c-cd0f-4dcd-ad65-9ec9b4b19c45)   
 [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
