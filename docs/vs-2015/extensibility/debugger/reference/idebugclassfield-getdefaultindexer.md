---
title: IDebugClassField::GetDefaultIndexer |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::GetDefaultIndexer
helpviewer_keywords:
- IDebugClassField::GetDefaultIndexer method
ms.assetid: 47ce4f45-3816-4b40-909c-5032d0692d75
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6be0a1925a1e5d48941c1c0e13ac1b4789687229
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191017"
---
# <a name="idebugclassfieldgetdefaultindexer"></a>IDebugClassField::GetDefaultIndexer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取默认索引器的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetDefaultIndexer(   
   BSTR* pbstrIndexer  
);  
```  
  
```csharp  
int GetDefaultIndexer(  
   out string pbstrIndexer  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pbstrIndexer`  
 [out]返回包含的默认索引器的名称的字符串。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK 或如果没有默认索引器，则返回 S_FALSE。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 一个类的默认索引器是属性，它被标记为`Default`数组访问的属性。 这是特定于[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]。 下面是一个示例中声明的默认索引器[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]以及如何使用它。  
  
```vb  
Imports System.Collections;  
  
Public Class Class1  
    Private myList as Hashtable  
  
    Default Public Property Item(ByVal Index As Integer) As Integer  
        Get  
            Return CType(List(Index), Integer)  
        End Get  
        Set(ByVal Value As Integer)  
            List(Index) = Value  
        End Set  
    End Property  
End Class  
  
Function GetItem(Index as Integer) as Integer  
    Dim classList as Class1 = new Class1  
    Dim value as Integer  
  
    ' Access array through default indexer  
    value = classList(2)  
  
    ' Access array through explicit property  
    value = classList.Item(2)  
  
    Return value  
End Function  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
