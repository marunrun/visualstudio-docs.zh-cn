---
title: POPLISTFUNC |Microsoft Docs
description: 了解 POPLISTFUNC 回调函数，该函数由源代码管理插件用来更新文件或目录的列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 239f1aa5a55c3a5ce3a0f2a3ec9145f3cdb0630e
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863164"
---
# <a name="poplistfunc"></a>POPLISTFUNC
此回调由 IDE 提供给 [SccPopulateList](../extensibility/sccpopulatelist-function.md) ，由源代码管理插件用来更新) 提供给函数的文件或 (目录的列表 `SccPopulateList` 。

 当用户在 IDE 中选择 " **获取** " 命令时，ide 将显示用户可获取的所有文件的列表框。 遗憾的是，IDE 并不知道用户可能获得的所有文件的确切列表;只有该插件具有此列表。 如果其他用户已将文件添加到源代码管理项目，则这些文件应显示在列表中，但 IDE 不知道它们。 IDE 会生成一个列表，其中列出了用户可以获取的文件。 在向用户显示此列表之前，它将调用[SccPopulateList](../extensibility/sccpopulatelist-function.md) ， `,` 使源代码管理插件有机会在列表中添加和删除文件。

## <a name="signature"></a>签名
 源代码管理插件通过使用以下原型调用 IDE 实现的函数来修改列表：

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>参数
 pvCallerData `pvCallerData` 调用方传递的参数 (IDE) 发送到 [SccPopulateList](../extensibility/sccpopulatelist-function.md)。 源代码管理插件应该不会对此参数的内容进行任何假设。

 如果 `TRUE` 为， `lpFileName` 则为 fAddRemove，它是应添加到文件列表中的文件。 如果 `FALSE` `lpFileName` 为，则为应从文件列表中删除的文件。

 nStatus 状态 `lpFileName` (位的组合; 有关 `SCC_STATUS` 详细信息，请参阅 [文件状态代码](../extensibility/file-status-code-enumerator.md)) 。

 lpFileName 要在列表中添加或删除的文件名的完整目录路径。

## <a name="return-value"></a>返回值

|值|说明|
|-----------|-----------------|
|`TRUE`|插件可以继续调用此函数。|
|`FALSE`|IDE 端出现问题 (如) 内存不足的情况。 插件应停止操作。|

## <a name="remarks"></a>备注
 对于源代码管理插件要在文件列表中添加或删除的每个文件，它将调用此函数，并传入 `lpFileName` 。 `fAddRemove`标志指示要添加到列表中的新文件或要删除的旧文件。 `nStatus`参数提供文件的状态。 当 SCC 插件完成添加和删除文件时，它将从 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 调用返回。

> [!NOTE]
> `SCC_CAP_POPULATELIST`功能位是 Visual Studio 所必需的。

## <a name="see-also"></a>另请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
