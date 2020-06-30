---
title: GetAutoInsertExtensions 方法
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f5d88af6f24306b7b243359c9797a2cb7e7449bc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543502"
---
# <a name="getautoinsertextensions-method"></a>GetAutoInsertExtensions 方法
  获取有关在调试过程中将自动插入的 Office 相关应用程序的信息。

 此方法保留供将来使用。

## <a name="syntax"></a>语法

```csharp
HRESULT GetAutoInsertExtensions(
    [out, retval] SAFEARRAY(BSTR)* psaExtensionNames
);
```

### <a name="parameters"></a>参数

|参数|说明|
|---------------|-----------------|
|*psaExtensionNames*|适用于 Office 的应用程序的扩展名称。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 要插入的每个 Office 应用都作为 Office 应用程序扩展名称返回，这与**HKEY_CURRENT_USER \software\microsoft\office\wef\developer**下的值相对应。 宿主必须在注册表中查找这些值，然后自动插入扩展。
