---
title: IDebugSourceServerModule | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugSourceServerModule interface
ms.assetid: 38213060-451d-46e6-8b4a-efc123e01a2c
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0dec9408d0cd1907a533a8cabe740832fe652398
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555685"
---
# <a name="idebugsourceservermodule"></a>IDebugSourceServerModule
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示包含在 PDB 文件中的源服务器信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugSourceServerModule : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 此接口是由调试器引擎实现，由调试器用户界面。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugSourceServerModule`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetSourceServerData](../../../extensibility/debugger/reference/idebugsourceservermodule-getsourceserverdata.md)|检索源服务器信息的数组。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
