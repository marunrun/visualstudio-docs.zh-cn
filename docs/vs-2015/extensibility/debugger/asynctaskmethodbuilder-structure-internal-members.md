---
title: AsyncTaskMethodBuilder 结构-内部成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncTaskMethodBuilder structure [.NET Framework]
- AsyncTaskMethodBuilder structure [.NET Framework debug engines]
ms.assetid: f32f5857-7ef8-45fd-8b5a-7f644eb98b11
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bfe640654c9de7daac9096aa4d75f5492a8a278
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555907"
---
# <a name="asynctaskmethodbuilder-structure---internal-members"></a>AsyncTaskMethodBuilder 结构 - 内部成员
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题介绍的内部成员的<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>类。 有关此类的常规信息，请参阅<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>参考主题。  
  
 **Namespace**：<xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder  
       extends System.ValueType  
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder  
```  
  
## <a name="internal-members"></a>内部成员  
  
|名称|描述|  
|----------|-----------------|  
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-objectidfordebugger-property.md)|获取可用于唯一地标识调试器到此生成器的对象。|  
|[m_builder 字段](../../extensibility/debugger/asynctaskmethodbuilder-m-builder-field.md)|表示此非泛型实例委托的泛型生成器对象。|  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder>   
 [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
