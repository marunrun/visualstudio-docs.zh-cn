---
title: 创建源代码管理插件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 37cb4cfc71b2574600bf7ca886c693b888ec821a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196965"
---
# <a name="creating-a-source-control-plug-in"></a>创建源代码管理插件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio SDK 提供了一些资源，可用于将源代码管理功能添加到 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] (IDE) 的集成开发环境。 它允许你使用任何符合本文档中所述源代码管理插件 API 的插件 DLL。  
  
## <a name="in-this-section"></a>本节内容  
 [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)  
 描述如何安装源代码管理插件并突出显示当前可用的源代码管理插件 API 版本。  
  
 [体系结构](../../extensibility/internals/source-control-plug-in-architecture.md)  
 使用体系结构关系图说明源代码管理插件与 IDE 的集成 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 [源代码管理插件的测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 提供有关如何测试源代码管理插件的安装和操作的指导。  
  
## <a name="related-sections"></a>相关章节  
 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 讨论如何创建一个源代码管理 VSPackage，该控件不仅提供源代码管理功能，而且还替换 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 源代码管理 UI。  
  
 [源代码管理插件](../../extensibility/source-control-plug-ins.md)  
 提供源代码管理插件 API 中所有元素的完整列表。  
  
 [源代码管理](../../extensibility/internals/source-control.md)  
 讨论用于实现作为的集成功能的源代码管理的选项 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。
