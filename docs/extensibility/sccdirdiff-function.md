---
title: SccDirDiff 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701017"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 函数
此函数显示客户端磁盘上的当前本地目录与源代码管理下的相应项目之间的差异。

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

中源代码管理插件上下文结构。

 hWnd

中IDE 窗口的句柄，源代码管理插件可将其用作它所提供的所有对话框的父级。

 lpDirName

中要显示其视觉对象差异的本地目录的完全限定路径。

 dwFlags 

中命令标志 (参阅) 的 "备注" 部分。

 pvOptions

中源代码管理插件特定的选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|磁盘上的目录与源代码管理中的项目相同。|
|SCC_I_FILESDIFFER|磁盘上的目录不同于源代码管理中的项目。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|此目录不受源代码管理。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题导致的。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|
|SCC_E_FILENOTEXIST|找不到本地目录。|

## <a name="remarks"></a>备注
 此函数用于指示源代码管理插件向用户显示对指定目录的更改列表。 插件以其选择的格式打开其自己的窗口，以显示用户在磁盘上的目录与版本控制下的相应项目之间的差异。

 如果插件支持完全比较目录，则即使不支持 "快速差异" 选项，它也必须支持文件名称的比较。

|`dwFlags`|解释|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|不区分大小写的比较 (可用于快速差异或 visual) 。|
|SCC_DIFF_IGNORESPACE|忽略空白 (可用于快速差异或视觉) 。|
|SCC_DIFF_QD_CONTENTS|如果源代码管理插件支持，则以无提示方式按字节对目录进行比较。|
|SCC_DIFF_QD_CHECKSUM|如果插件支持，则通过校验和来自动比较目录，或者，如果不支持，则回退到 SCC_DIFF_QD_CONTENTS。|
|SCC_DIFF_QD_TIME|如果插件支持此模式，则会通过其时间戳自动比较目录，或者，如果不支持，则会回退 SCC_DIFF_QD_CHECKSUM 或 SCC_DIFF_QD_CONTENTS。|

> [!NOTE]
> 此函数使用与 [SccDiff](../extensibility/sccdiff-function.md)相同的命令标志。 但是，源代码管理插件可能会选择不支持目录的 "快速差异" 操作。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
