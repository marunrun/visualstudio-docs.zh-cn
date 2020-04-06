---
title: SccDirDiff 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1bb592a1174a91480ed76ef818733c288c5273c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701017"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 函数
此功能显示客户端磁盘上的当前本地目录与源代码管理下的相应项目之间的差异。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccDirDiff(
   LPVOID    pContext,
   HWND      hWnd,
   LPCSTR    lpDirName,
   LONG      dwFlags,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 lpDirname

[在]本地目录的完全限定路径，用于显示视觉差异。

 dwFlags

[在]命令标志（请参阅备注部分）。

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|磁盘上的目录与源代码管理中的项目相同。|
|SCC_I_FILESDIFFER|磁盘上的目录与源代码管理中的项目不同。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|目录不受源代码控制。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特异性故障。|
|SCC_E_FILENOTEXIST|找不到本地目录。|

## <a name="remarks"></a>备注
 此功能用于指示源代码管理插件向用户显示对指定目录的更改列表。 该插件以其选择的格式打开自己的窗口，以显示用户在磁盘上的目录与版本控制下的相应项目之间的差异。

 如果插件根本不支持目录的比较，则即使不支持"快速差异"选项，它也必须支持基于文件名对目录进行比较。

|`dwFlags`|解释|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|区分大小写的比较（可用于快速差异或视觉）。|
|SCC_DIFF_IGNORESPACE|忽略空白（可用于快速差异或视觉）。|
|SCC_DIFF_QD_CONTENTS|如果源代码管理插件支持，请静默地比较目录，字节字节。|
|SCC_DIFF_QD_CHECKSUM|如果插件支持，则通过校验和静静比较目录，或者，如果不支持，则回落到SCC_DIFF_QD_CONTENTS。|
|SCC_DIFF_QD_TIME|如果插件支持，请通过其时间戳静静比较目录，或者，如果不支持，则落在SCC_DIFF_QD_CHECKSUM或SCC_DIFF_QD_CONTENTS。|

> [!NOTE]
> 此函数使用与[SccDiff](../extensibility/sccdiff-function.md)相同的命令标志。 但是，源代码管理插件可以选择不支持目录的"快速差异"操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
