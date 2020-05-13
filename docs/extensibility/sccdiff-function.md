---
title: SccDiff 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9b68df68ce7fa4ad5cbc98db256204ddf8623d2c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701026"
---
# <a name="sccdiff-function"></a>SccDiff 函数
此函数显示（或可选地只检查）当前文件（本地磁盘上）与其在源代码管理系统中的最后签入版本之间的差异。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDiff(
   LPVOID    pvContext,
   HWND      hWnd,
   LPCSTR    lpFileName,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpFile名称

[在]请求差异的文件名。

 fOptions

[在]命令标志。 有关详细信息，请参阅备注。

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|工作副本和服务器版本相同。|
|SCC_I_FILESDIFFERS|工作副本与源代码管理下的版本不同。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|该文件不受源代码管理。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特异性故障;未获取文件差异。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 此功能具有两种不同的用途。 默认情况下，它显示对文件的更改列表。 源代码管理插件以您选择的任何格式打开自己的窗口，以显示用户在磁盘上的文件与源代码管理下文件的最新版本之间的差异。

 或者，IDE 可能只需要确定文件是否已更改。 例如，IDE 可能需要确定在未通知用户的情况下签出文件是否安全。 在这种情况下，IDE 会传递标志`SCC_DIFF_CONTENTS`。 源代码管理插件必须对照源代码管理的文件检查磁盘上的文件字节，并返回一个值，指示两个文件是否不同而不向用户显示任何内容。

 作为性能优化，源代码管理插件可以使用基于校验和或时间戳的替代方法，而不是：`SCC_DIFF_CONTENTS`这些比较形式显然更快但不太可靠。 并非所有源代码管理系统都支持这些替代比较方法，插件可能必须回到内容比较。 所有源代码管理插件必须至少支持内容比较。

> [!NOTE]
> 快速差异标志是互斥的。 不传递任何标志是有效的，但同时传递多个标志无效。 `SCC_DIFF_QUICK_DIFF`，这是一个包含所有标志的掩码，可用于测试，但绝不应作为参数传递。

|`fOption`|含义|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|区分大小写的比较（可用于快速或视觉差异）。|
|SCC_DIFF_IGNORESPACE|忽略空白（可用于快速或视觉差异）。|
|SCC_DIFF_QD_CONTENTS|静默比较文件，字节字节。|
|SCC_DIFF_QD_CHECKSUM|在支持时，通过校验和静静比较文件。 如果不支持，则回落到内容的比较。|
|SCC_DIFF_QD_TIME|在支持时，通过时间戳悄悄地比较文件。 如果不支持，则回落到内容的比较。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
