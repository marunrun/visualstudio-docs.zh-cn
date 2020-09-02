---
title: 入门源代码管理插件 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62538156"
---
# <a name="getting-started-with-source-control-plug-ins"></a>源代码管理插件入门
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要创建源代码管理插件，您必须创建一个 DLL 来实现源代码管理插件 API 中定义的函数，然后将该 DLL 注册 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 到，使其可在源代码版本控制中使用。  
  
 源代码管理插件 API 的三个版本 (版本1.1、1.2 和 1.3) 可用于源代码管理插件。此处所述的源代码管理插件 API 是版本1.3。 它设计为与支持1.1 和1.2 版本的源代码管理插件完全兼容。 [源代码管理插件 Api 版本1.3 中的新增](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)功能部分详细介绍了最新版本的源代码管理插件 api 中支持的新增功能。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)  
 介绍如何创建插入源代码管理 DLL 所需的注册表项。  
  
 [源代码管理插件 API 版本 1.3 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-3.md)  
 简要概述版本1.3 中对源代码管理插件 API 所做的更改。  
  
 [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)  
 简要概述版本1.2 中对源代码管理插件 API 所做的更改。  
  
## <a name="related-sections"></a>相关章节  
 [源代码管理插件](../../extensibility/source-control-plug-ins.md)  
 提供源代码管理插件 API 中所有元素的完整列表。  
  
 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 定义源代码管理插件 SDK 并介绍所包含的资源。
