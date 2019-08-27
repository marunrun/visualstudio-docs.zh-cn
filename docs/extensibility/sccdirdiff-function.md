---
title: SccDirDiff 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c3d207a171acba4127849cd479a1049afafa8492
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351901"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 函数
此函数显示在客户端磁盘上的当前本地目录与源代码管理下的相应项目之间的差异。

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 lpDirName

[in]要为其显示 visual 差异的本地目录的完全限定的路径。

 dwFlags

[in]命令标志 (请参阅备注部分)。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|在磁盘上的目录是在源代码管理中的项目相同。|
|SCC_I_FILESDIFFER|从源代码管理中的项目不同磁盘上的目录。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|目录不受源代码管理中。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|
|SCC_E_FILENOTEXIST|找不到本地目录。|

## <a name="remarks"></a>备注
 此函数用于指示源代码管理插件以向用户显示的更改到指定的目录列表。 该插件，则将其自己的窗口，打开格式为它选择显示磁盘上的用户的目录和版本控制下的相应项目之间的差异。

 如果插件支持的所有目录的比较，它必须在文件名称的基础上支持的目录的比较，即使不支持"快速 diff"选项。

|`dwFlags`|解释|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|（可能使用的快速差异或视觉对象） 的比较不区分大小写。|
|SCC_DIFF_IGNORESPACE|将忽略空白区域 （可能使用的快速差异或视觉对象）。|
|SCC_DIFF_QD_CONTENTS|如果受源代码管理插件，以无提示方式将目录中，按字节进行比较。|
|SCC_DIFF_QD_CHECKSUM|如果支持的插件，以无提示方式进行比较校验和，通过目录或，如果不受支持，回退到 SCC_DIFF_QD_CONTENTS。|
|SCC_DIFF_QD_TIME|如果插件支持，以无提示方式比较其时间戳，通过目录或者，如果不受支持，将回退 SCC_DIFF_QD_CHECKSUM 或 SCC_DIFF_QD_CONTENTS 上。|

> [!NOTE]
> 此函数使用相同的命令标志，作为[SccDiff](../extensibility/sccdiff-function.md)。 但是，可以选择源代码管理插件不支持目录的"快速 diff"操作。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)