---
title: SccDiff 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52da17cbb7f6349d99a04709bbe469501394d4e5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327508"
---
# <a name="sccdiff-function"></a>SccDiff 函数
此函数显示 （或根据需要只需检查） 控制系统的源中的当前文件 （在本地磁盘） 和其最后一个签入的版本之间的差异。

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

[in]源控制插件上下文结构。

 hWnd

[in]它提供了任何对话框，父级可以使用源代码管理插件，则 IDE 窗口的句柄。

 lpFileName

[in]为其请求不同之处的文件名。

 fOptions

[in]命令的标志。 有关详细信息，请参阅备注。

 pvOptions

[in]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|工作副本和服务器版本是相同的。|
|SCC_I_FILESDIFFERS|工作副本与受源代码管理版本不同。|
|SCC_I_RELOADFILE|需要重新加载文件或项目。|
|SCC_E_FILENOTCONTROLLED|文件不是源代码管理下。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统，很可能是由于网络或争用问题时出现问题时。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障;无法获得文件差异。|
|SCC_E_FILENOTEXIST|找不到本地文件。|

## <a name="remarks"></a>备注
 此函数有两个不同的用途。 默认情况下，它为文件显示更改的列表。 源代码管理插件将自己的窗口，打开任何格式选择，则显示磁盘上的用户的文件和源代码管理下的文件的最新版本之间的差异。

 或者，在 IDE 可能只被需要确定文件是否已更改。 例如，在 IDE 可能需要确定它是否可以安全地签出文件，而无需通知用户。 在这种情况下，IDE 将传入`SCC_DIFF_CONTENTS`标志。 源代码管理插件必须检查该文件在磁盘上，按字节，针对受源代码管理文件并返回一个值，该值指示两个文件是否不同而不会向用户显示任何内容。

 作为一种性能优化，源代码管理插件可能会使用基于校验和或时间戳而不是逐字节比较的所要求的替代方法`SCC_DIFF_CONTENTS`： 这些形式的比较都是很明显更快，但可靠性较低。 并非所有的源代码管理系统可能支持这些替代比较方法，并且该插件可能要故障回复到的内容比较。 所有源代码管理插件，至少必须都支持的内容比较。

> [!NOTE]
> 快速差异标志是互斥的。 有效地不传递任何标志，但它不是有效地同时传递多个。 `SCC_DIFF_QUICK_DIFF`它一个屏蔽，它结合了所有标志，可用于测试，但永远不应作为参数传递。

|`fOption`|含义|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|（可能为快速或视觉对象使用） 的比较不区分大小写。|
|SCC_DIFF_IGNORESPACE|将忽略空白区域 （可能为快速或视觉对象使用）。|
|SCC_DIFF_QD_CONTENTS|以无提示方式将该文件，按字节进行比较。|
|SCC_DIFF_QD_CHECKSUM|以无提示方式将通过校验和时支持的文件进行比较。 如果不受支持，回退到的内容比较。|
|SCC_DIFF_QD_TIME|以无提示方式将通过其时间戳时支持的文件进行比较。 如果不受支持，回退到的内容比较。|

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)