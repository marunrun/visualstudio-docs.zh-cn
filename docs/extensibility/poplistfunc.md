---
title: POPLISTFUNC |微软文档
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
ms.openlocfilehash: 6c5f8c1683a993915476ff23f1f5d5f2c2aba462
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702066"
---
# <a name="poplistfunc"></a>POPLISTFUNC
此回调由 IDE 提供给[SccPopulateList，](../extensibility/sccpopulatelist-function.md)源代码管理插件用于更新文件或目录的列表（也提供给`SccPopulateList`函数）。

 当用户在 IDE 中选择**Get**命令时，IDE 将显示用户可以获取的所有文件的列表框。 遗憾的是，IDE 不知道用户可能获得的所有文件的确切列表;只有插件有此列表。 如果其他用户将文件添加到源代码管理项目，这些文件应出现在列表中，但 IDE 不知道它们。 IDE 生成它认为用户可以获取的文件的列表。 在向用户显示此列表之前，它会调用[SccPopulateList，](../extensibility/sccpopulatelist-function.md)`,`使源代码管理插件有机会从列表中添加和删除文件。

## <a name="signature"></a>签名
 源代码管理插件通过使用以下原型调用 IDE 实现函数来修改列表：

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>参数
 pvCallerData`pvCallerData`调用方 （IDE） 传递给[SccpopulateList 的](../extensibility/sccpopulatelist-function.md)参数。 源代码管理插件不应假定此参数的内容。

 fAddRemove `TRUE`If `lpFileName` ， 是应添加到文件列表中的文件。 如果`FALSE``lpFileName`是应从文件列表中删除的文件。

 n 状态`lpFileName`状态（`SCC_STATUS`位的组合;有关详细信息，请参阅[文件状态代码](../extensibility/file-status-code-enumerator.md)）。

 lpFileName 文件名的完整目录路径，以便从列表中添加或删除。

## <a name="return-value"></a>返回值

|值|说明|
|-----------|-----------------|
|`TRUE`|插件可以继续调用此功能。|
|`FALSE`|IDE 端出现问题（如内存不足情况）。 插件应停止操作。|

## <a name="remarks"></a>备注
 对于源代码管理插件要添加到文件列表中或删除的每个文件，它将调用此函数，传入`lpFileName`。 该`fAddRemove`标志指示要添加到列表的新文件或要删除的旧文件。 参数`nStatus`提供文件的状态。 当 SCC 插件完成添加和删除文件后，它将从[SccPopulateList](../extensibility/sccpopulatelist-function.md)调用返回。

> [!NOTE]
> 可视化`SCC_CAP_POPULATELIST`工作室需要功能位。

## <a name="see-also"></a>请参阅
- [IDE 实现的回调功能](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [文件状态代码](../extensibility/file-status-code-enumerator.md)
