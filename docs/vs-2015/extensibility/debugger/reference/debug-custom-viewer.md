---
title: DEBUG_CUSTOM_VIEWER | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d10e0811044d7169eaf46f48f53389fa7b3076ec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179171"
---
# <a name="debugcustomviewer"></a>DEBUG_CUSTOM_VIEWER
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

标识自定义查看器的结构或类型可视化工具。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct tagDEBUG_CUSTOM_VIEWER {  
   DWORD dwID;  
   BSTR  bstrMenuName;  
   BSTR  bstrDescription;  
   GUID  guidLang;  
   GUID  guidVendor;  
   BSTR  bstrMetric;  
} DEBUG_CUSTOM_VIEWER;  
```  
  
```csharp  
public struct DEBUG_CUSTOM_VIEWER {  
   public uint   dwID;  
   public string bstrMenuName;  
   public string bstrDescription;  
   public Guid   guidLang;  
   public Guid   guidVendor;  
   public string bstrMetric;  
};  
```  
  
## <a name="members"></a>成员  
 dwID  
 一个 ID 来区分多个查看器或实现一个可视化工具`GUID`。  
  
 bstrMenuName  
 将出现在下拉列表菜单文本。  
  
 bstrDescription  
 如果未使用 （必须为 null 值） 的类型可视化工具的自定义查看器的说明。  
  
 guidLang  
 提供的表达式计算器的语言。  
  
 guidVendor  
 提供的表达式计算器的供应商。  
  
 bstrMetric  
 指标在其下的自定义查看器或类型可视化工具`CLSID`存储。  
  
## <a name="remarks"></a>备注  
 此结构的列表返回通过调用[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法 (以及由此而[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法)。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
