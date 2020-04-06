---
title: SccSetOption 功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1adcbb47e9fce7037fe8942326e8836ade51e3eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700314"
---
# <a name="sccsetoption-function"></a>SccSetOption 函数
此函数设置控制源代码管理插件行为的选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccSetOption(
   LPVOID pvContext,
   LONG   nOption,
   LONG   dwVal
);
```

#### <a name="parameters"></a>参数
 pvContext

[在]源代码管理插件上下文结构。

 nOption

[在]正在设置的选项。

 德瓦尔

[在]选项的设置。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功设置该选项。|
|SCC_I_SHARESUBPROJOK|返回（`nOption`如果是`SCC_OPT_SHARESUBPROJ`）和源代码管理插件允许 IDE 设置目标文件夹。|
|SCC_E_OPNOTSUPPORTED|该选项未设置，不应依赖。|

## <a name="remarks"></a>备注
 IDE 调用此函数以控制源代码管理插件的行为。 第一个参数`nOption`， 指示要设置的值， 而第二个`dwVal`参数 指示如何处理该值。 插件存储与 的此信息相关联，`pvContext``,`因此 IDE 必须在调用 Scc 初始化后调用此函数（但不一定在每次调用[SccOpenProject](../extensibility/sccopenproject-function.md)后）。 [SccInitialize](../extensibility/sccinitialize-function.md)

 选项及其值的摘要：

|`nOption`|`dwValue`|描述|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|启用/禁用后台事件队列。|
|`SCC_OPT_USERDATA`|任意值|指定要传递给[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)回调功能的用户值。|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|指示 IDE 当前是否支持取消操作。|
|`SCC_OPT_NAMECHANGEPFN`|指向[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)回调函数的指针|设置指向名称更改回调函数的指针。|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|指示 IDE 是否允许手动签出其文件（通过源代码管理用户界面），或者是否必须通过源代码管理插件签出这些文件。|
|`SCC_OPT_SHARESUBPROJ`|空值|如果源代码管理插件允许 IDE 指定本地项目文件夹，则插件将返回`SCC_I_SHARESUBPROJOK`。|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 如果是`nOption``SCC_OPT_EVENTQUEUE`，IDE 正在禁用（或重新启用）后台处理。 例如，在编译期间，IDE 可能会指示源代码管理插件停止任何类型的空闲处理。 编译后，它将重新启用后台处理，以使插件的事件队列保持最新。 `SCC_OPT_EVENTQUEUE`对应于`nOption`的值 ， 有两个可能的值`dwVal`， 和`SCC_OPT_EQ_ENABLE`。 `SCC_OPT_EQ_DISABLE`

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 如果 值`nOption`为`SCC_OPT_HASCANCELMODE`，IDE 允许用户取消长操作。 设置为`dwVal``SCC_OPT_HCM_NO`（默认值）表示 IDE 没有取消模式。 源代码管理插件必须提供自己的"取消"按钮，如果用户希望用户能够取消。 `SCC_OPT_HCM_YES`指示 IDE 提供了取消操作的功能，因此 SCC 插件不需要显示其自己的"取消"按钮。 如果 IDE`dwVal`将`SCC_OPT_HCM_YES`设置到 ，则它准备`SCC_MSG_STATUS`响应`DOCANCEL`回调函数并发送消息`lpTextOutProc`（请参阅[LPTEXTOUTPROC）。](../extensibility/lptextoutproc.md) 如果 IDE 未设置此变量，插件不应发送这两条消息。

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 如果 nOption 设置为`SCC_OPT_NAMECHANGEPFN`，并且源代码管理插件和 IDE 都允许它，则插件实际上可以在源代码管理操作期间重命名或移动文件。 `dwVal`将设置为[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)类型的函数指针。 在源代码管理操作期间，插件可以调用此函数，传递三个参数。 这些是文件的旧名称（具有完全限定的路径），该文件的新名称（具有完全限定的路径），以及指向与 IDE 相关的信息的指针。 IDE`SccSetOption`通过调用 设置为`nOption``SCC_OPT_USERDATA`（） 发送此最后一`dwVal`个指针，并指向数据。 支持此功能是可选的。 使用此功能的 VSSCI 插件必须将其函数指针和用户数据变量初始化到`NULL`，除非已授予它，否则不得调用重命名函数。 它还应准备保留所给出的值，或更改该值以响应对`SccSetOption`的新调用。 这在源代码管理命令操作中不会发生，但可能在命令之间发生。

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 如果 nOption 设置为`SCC_OPT_SCCCHECKOUTONLY`，IDE 表示不应通过源代码管理系统的用户界面手动签出当前打开项目中的文件。 相反，文件应仅通过 IDE 控制下的源代码管理插件签出。 如果`dwValue`设置为`SCC_OPT_SCO_NO`，则意味着插件应正常处理文件，并且可以通过源代码管理 UI 签出文件。 如果`dwValue`设置为`SCC_OPT_SCO_YES`，则只允许插件签出文件，并且不应调用源代码管理系统的 UI。 这是针对 IDE 可能具有"伪文件"的情况，这些"伪文件"仅通过 IDE 签出才有意义。

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 如果`nOption`设置为`SCC_OPT_SHARESUBPROJ`，IDE 正在测试源代码管理插件在从源代码管理添加文件时是否可以使用指定的本地文件夹。 在这种情况下，`dwVal`参数的值并不重要。 如果插件允许 IDE 指定在调用[SccAddFromScc](../extensibility/sccaddfromscc-function.md)时从源代码管理中添加文件的本地目标文件夹，则该插件必须在调用`SCC_I_SHARESUBPROJOK``SccSetOption`该函数时返回。 然后，IDE 使用`lplpFileNames`函数的`SccAddFromScc`参数在目标文件夹中传递。 该插件使用该目标文件夹来放置从源代码管理添加的文件。 如果设置`SCC_OPT_SHARESUBPROJ`该选项时插件未返回`SCC_I_SHARESUBPROJOK`，IDE 假定该插件只能在当前本地文件夹中添加文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
