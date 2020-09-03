---
title: m_children 字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 749b7a8da2cbdf8377e7f2e1fcb39787e2f42303
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149064"
---
# <a name="m_children-field"></a>m_children 字段
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

向此任务注册的子任务的列表。  
  
 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **Assembly：** mscorlib (mscorlib.dll)   
  
 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。  
  
## <a name="syntax"></a>语法  
  
```  
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children  
```  
  
## <a name="remarks"></a>备注  
 当任务正在运行时，只有执行任务的线程才能访问此数组。  
  
 如果任务已完成，则其他线程可以访问此字段，前提是它们不会向其添加任何内容或从中删除任何内容。  
  
## <a name="see-also"></a>另请参阅  
 [ContingentProperties 类](../../extensibility/debugger/contingentproperties-class-internal-members.md)
