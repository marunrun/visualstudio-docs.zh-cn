---
title: 开始使用源代码管理插件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, getting started
- getting started, source control plug-ins
ms.assetid: 46ac1f9f-4ecc-4a72-88d3-4c7e1647e1cb
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 85aa5727f252ad75c45064d7b885e3d282da36a4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538156"
---
# <a name="getting-started-with-source-control-plug-ins"></a>源代码管理插件入门
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要创建源代码管理插件，必须创建实现源控件插件 API 中定义的函数的 DLL，然后注册与 DLL [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，使其可供使用源代码版本控制中。  
  
 三个版本的源控制插件 API （版本 1.1、 1.2 和 1.3） 可为源代码管理插件。此处的文档的源控制插件 API 是 1.3 版。 它的设计目标是与源代码管理插件完全兼容支持版本 1.1 和 1.2。 [What's New in 源控制插件 API 版本 1.3](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)部分详细介绍了最新版本的源控制插件 API 中支持的新功能。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)  
 介绍如何在源控件 DLL 中插入所需的注册表项。  
  
 [源代码管理插件 API 版本 1.3 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)  
 提供对源控制插件 API 版本 1.3 中所做的更改的简要概述。  
  
 [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)  
 提供对源控制插件 API 版本 1.2 中所做的更改的简要概述。  
  
## <a name="related-sections"></a>相关章节  
 [源代码管理插件](../../extensibility/source-control-plug-ins.md)  
 提供源控制插件 API 中的所有元素的完整列表。  
  
 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 定义源控制插件 SDK 并介绍了包含的资源。
