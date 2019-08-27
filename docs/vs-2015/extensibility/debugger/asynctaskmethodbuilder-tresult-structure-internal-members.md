---
title: AsyncTaskMethodBuilder&lt;TResult&gt;结构-内部成员 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7e4999b71ae8f654aa3d362ba16c6cf5bc6574da
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182267"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>AsyncTaskMethodBuilder&lt;TResult&gt;结构-内部成员
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本主题介绍的内部成员的<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>类。 有关此类的常规信息，请参阅<xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>参考主题。  
  
 **命名空间：** <xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
 **程序集：** mscorlib （在 mscorlib.dll 中)  
  
 无法从.NET Framework 来访问这些内部成员，因为以下语法提供通用中间语言 (CIL)。  
  
## <a name="syntax"></a>语法  
  
```  
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>  
       extends System.ValueType  
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder  
```  
  
## <a name="internal-members"></a>内部成员  
  
|名称|描述|  
|----------|-----------------|  
|[ObjectIdForDebugger 属性](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|获取可用于唯一地标识调试器到此生成器的对象。|  
|[m_task 字段](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|表示延迟初始化的生成任务。|  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>   
 [.NET Framework 的并行扩展内幕](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
