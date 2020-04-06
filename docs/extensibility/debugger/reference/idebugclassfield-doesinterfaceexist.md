---
title: IDebugClassField：:D接口存在 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba732b698f7372772142fda73e71d9e22aa443a6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734494"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
确定是否在类中定义了特定接口。

## <a name="syntax"></a>语法

```cpp
HRESULT DoesInterfaceExist( 
   LPCOLESTR pszInterfaceName
);
```

```csharp
int DoesInterfaceExist(
   [In] string pszInterfaceName
);
```

## <a name="parameters"></a>参数
`pszInterfaceName`\
[在]包含要查找的接口名称的字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK，如果接口不存在，则返回S_FALSE;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上获取所有接口的枚举，并搜索列表以寻找匹配的接口。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
