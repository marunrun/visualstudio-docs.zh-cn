---
title: SccGet 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2d69308d2f569fc2e0d72dcf64c762687955d4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700891"
---
# <a name="sccget-function"></a>SccGet 函数
此函数检索一个或多个文件的副本，用于查看和编译，但不用于编辑。 在大多数系统中，文件标记为只读。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件的上下文结构。

 hwnd

[在]源控件插件可以用作它提供的任何对话框的父级的 IDE 窗口句柄。

 n文件

[在]`lpFileNames`数组中指定的文件数。

 lpFile名称

[在]要检索的文件完全限定名称的数组。

 fOptions

[在]命令标志`SCC_GET_ALL`（。 `SCC_GET_RECURSIVE`

 pvOptions

[在]源代码管理插件特定选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功获得操作。|
|SCC_E_FILENOTCONTROLLED|该文件不受源代码管理。|
|SCC_E_OPNOTSUPPORTED|源代码管理系统不支持此操作。|
|SCC_E_FILEISCHECKEDOUT|无法获取用户当前已签出的文件。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，可能是由于网络或争用问题。 建议重试。|
|SCC_E_NOSPECIFIEDVERSION|指定无效的版本或日期/时间。|
|SCC_E_NONSPECIFICERROR|非特异性故障;文件未同步。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|
|SCC_E_NOTAUTHORIZED|用户无权执行此操作。|

## <a name="remarks"></a>备注
 此函数使用要检索的文件的计数和名称数组进行调用。 如果 IDE 传递标志`SCC_GET_ALL`，则意味着 中的`lpFileNames`项不是文件，而是目录，并且要检索给定目录中源控制下的所有文件。

 该`SCC_GET_ALL`标志可以与标志组合，`SCC_GET_RECURSIVE`以检索给定目录中的所有文件和所有子目录。

> [!NOTE]
> `SCC_GET_RECURSIVE`绝不应通过没有`SCC_GET_ALL`。 此外，请注意，如果目录*C：\A*和*C：\A\B*都传递递归获取，则*C：\A\B*及其所有子目录实际上将被检索两次。 IDE 有责任（而不是源代码管理插件）确保此类重复项远离阵列。

 最后，即使源代码管理插件在初始化时指定`SCC_CAP_GET_NOUI`了标志，表示它没有 Get 命令的用户界面，IDE 仍可能调用此功能来检索文件。 该标志仅表示 IDE 不显示 Get 菜单项，并且插件不应提供任何 UI。

## <a name="rename-files-and-sccget"></a>重命名文件和 SccGet
 情况：用户签出文件，例如*a.txt*，并修改该文件。 在可以签入*a.txt*之前，第二个用户将在源代码管理数据库中将*a.txt*重命名为*b.txt，* 签出*b.txt，* 对文件进行一些修改，然后签入该文件。 第一个用户希望第二个用户所做的更改，以便第一个用户将其本地版本的*a.txt*文件重命名为*b.txt，* 并执行文件获取。 但是，跟踪版本号的本地缓存仍然认为*a.txt*的第一个版本存储在本地，因此源代码管理无法解决这些差异。

 有两种方法可以解决此问题，即源代码管理版本的本地缓存与源代码管理数据库不同步：

1. 不允许重命名当前签出的源代码管理数据库中的文件。

2. 执行等效的"删除旧"后跟"添加新"。 以下算法是实现此目的的一种方法。

    1. 调用[SccQuery 更改](../extensibility/sccquerychanges-function.md)函数以了解在源代码管理数据库中将*a.txt*重命名为*b.txt。*

    2. 将本地*a.txt*重命名为*b.txt*。

    3. 调用`SccGet`*a.txt*和*b.txt 的*函数。

    4. 由于源代码管理数据库中不存在*a.txt，* 因此将清除缺少*的 a.txt*版本信息的本地版本缓存。

    5. 要签出的*b.txt*文件将与本地*b.txt*文件的内容合并。

    6. 现在可以签入更新的*b.txt*文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的比特标志](../extensibility/bitflags-used-by-specific-commands.md)
