---
title: SccDiff 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701026"
---
# <a name="sccdiff-function"></a>SccDiff 函数
此函数显示 (或选择性地检查) 本地磁盘) 上的当前文件 (与源代码管理系统中上次签入版本之间的差异。

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

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpFileName

中为其请求差异的文件名。

 用于

中命令标志。 有关详细信息，请参阅备注。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|工作副本和服务器版本是相同的。|
|SCC_I_FILESDIFFERS|工作副本不同于源代码管理下的版本。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|此文件不受源代码管理。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR|模糊失败;未获得文件差异。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 此函数有两种不同的用途。 默认情况下，它会显示文件的更改列表。 源代码管理插件以所选择的任何格式打开其自己的窗口，以显示用户在磁盘上的文件与源代码管理下的最新文件版本之间的差异。

 或者，IDE 可能只需要确定文件是否已更改。 例如，IDE 可能需要确定在不通知用户的情况下签出文件是否是安全的。 在这种情况下，IDE 会传入 `SCC_DIFF_CONTENTS` 标志。 源代码管理插件必须根据源代码管理的文件在磁盘上逐字节检查文件，并返回一个值，该值指示两个文件是否不同，而不会向用户显示任何内容。

 作为一种性能优化，源代码管理插件可能会基于校验和或时间戳使用一种替代方法，而不是由调用的按字节进行的比较 `SCC_DIFF_CONTENTS` 并非所有源代码管理系统都能支持这些备用的比较方法，而且插件可能不得不回退到内容比较。 所有源代码管理插件都必须至少支持内容比较。

> [!NOTE]
> 快速差异标志是互斥的。 传递无标志是有效的，但同时传递多个标记是无效的。 `SCC_DIFF_QUICK_DIFF`，它是合并所有标志的掩码，可用于测试，但绝不应作为参数传递。

|`fOption`|含义|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|不区分大小写的比较 (可用于快速或直观差异) 。|
|SCC_DIFF_IGNORESPACE|忽略空格 (可用于快速或视觉对象差异) 。|
|SCC_DIFF_QD_CONTENTS|以无提示方式按字节对文件进行比较。|
|SCC_DIFF_QD_CHECKSUM|如果受支持，则通过校验和自动比较文件。 如果不支持，将回退到内容的比较。|
|SCC_DIFF_QD_TIME|如果文件受支持，则以无提示方式对文件进行比较。 如果不支持，将回退到内容的比较。|

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
