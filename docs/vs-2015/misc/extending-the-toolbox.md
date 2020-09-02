---
title: 扩展工具箱 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- tools [Visual Studio], Toolbox
- Toolbox [Visual Studio SDK]
ms.assetid: bb84a79e-cd4c-4a58-8871-2513e7119b6e
caps.latest.revision: 38
manager: jillfra
ms.openlocfilehash: ddf67fba3ae603dbd31d4628c61a6f14cc2441c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686935"
---
# <a name="extending-the-toolbox"></a>扩展工具箱
[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **工具箱** 提供了一系列对象，这些对象通过 IDE 拖放机制为编辑器和设计器提供各种功能。  
  
 VSPackage 与 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **工具箱**联合使用有两种基本方式：  
  
- VSPackage 可以向 **工具箱**添加新数据项和控件。  
  
- VSPackage 可以是现有 **工具箱** 功能目标或使用者，支持拖放操作并配置 **工具箱**的外观。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：创建使用 Windows 窗体的工具箱控件](../misc/how-to-create-a-toolbox-control-that-uses-windows-forms.md)  
 描述出通过使用 Windows 窗体工具箱控件模板来创建工具箱控件。  
  
 [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)  
 描述出通过使用 WPF 工具箱控件模板来创建工具箱控件。  
  
 [管理工具箱](../misc/managing-the-toolbox.md)  
 介绍 VSPackage 管理 **工具箱**的内容和外观的方式。  
  
## <a name="related-sections"></a>相关章节  
 [如何：管理“工具箱”窗口](https://msdn.microsoft.com/a022c3fe-298c-4a59-a48f-b050da90ebc2)  
 介绍如何使用 **集成开发环境 (IDE) 中的** 工具箱 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
 [How to: Control the Toolbox](https://msdn.microsoft.com/library/c9d8a18a-d2bc-43d4-a803-601bfc6a6599)  
 介绍如何使用自动化编程模型管理 **工具箱** 。  
  
 [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)  
 说明如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 服务创建匹配 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的其余部分的 UI 元素。