---
title: 源代码管理 VSPackage 设计元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, design elements
ms.assetid: edd3f2ff-ca32-4465-8ace-4330493b67bb
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 06cd4523f91c341029140764b31fbd0ee262d551
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155680"
---
# <a name="source-control-vspackage-design-elements"></a>源代码管理 VSPackage 设计元素
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在本部分中的主题概述了结构源代码管理 VSPackage 必须实现的深度集成。 它还列出了这些接口和源代码管理 VSPackage 的服务可以实现，和源代码管理 VSPackage 的接口和服务可以使用从其他[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]组件来支持其源控制模型和功能。  
  
## <a name="in-this-section"></a>本节内容  
 [VSPackage 结构](../../extensibility/internals/vspackage-structure-source-control-vspackage.md)  
 定义源代码管理 VSPackage 的结构。  
  
 [相关服务和接口](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)  
 列出了源控制与包相关接口和服务。  
  
 [提供的服务](../../extensibility/internals/services-provided-source-control-vspackage.md)  
 描述由源代码管理 VSPackage 提供的源控制服务。  
  
## <a name="related-sections"></a>相关章节  
 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)  
 讨论如何创建源代码管理 VSPackage 不仅提供源代码管理功能，但可用于自定义[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]源代码管理 UI。
