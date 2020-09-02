---
title: SccSetOption 函数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7f2660ca99d8704f5dd8e7b9aa66c9c8fc5bdbb6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68143745"
---
# <a name="sccsetoption-function"></a>SccSetOption 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数设置控制源代码管理插件的行为的选项。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
SCCRTN SccSetOption(  
   LPVOID pvContext,  
   LONG   nOption,  
   LONG   dwVal  
);  
```  
  
#### <a name="parameters"></a>参数  
 pvContext  
 中源代码管理插件上下文结构。  
  
 nOption  
 中正在设置的选项。  
  
 dwVal  
 中选项的设置。  
  
## <a name="return-value"></a>返回值  
 此函数的源代码管理插件实现应返回以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|SCC_OK|已成功设置选项。|  
|SCC_I_SHARESUBPROJOK|如果 `nOption` 为 `SCC_OPT_SHARESUBPROJ` ，并且源代码管理插件允许 IDE 设置目标文件夹，则返回。|  
|SCC_E_OPNOTSUPPORTED|选项未设置，不应依赖。|  
  
## <a name="remarks"></a>备注  
 IDE 调用此函数来控制源代码管理插件的行为。 第一个参数 `nOption` 指示要设置的值，而第二个参数指示 `dwVal` 要如何处理该值。 插件存储与相关的此信息 `pvContext``,` ，因此，在调用 ([SccInitialize](../extensibility/sccinitialize-function.md) 之后，IDE 必须调用此函数，但不一定在每次调用 [SccOpenProject](../extensibility/sccopenproject-function.md)) 之后调用此函数。  
  
 选项及其值的摘要：  
  
|`nOption`|`dwValue`|说明|  
|---------------|---------------|-----------------|  
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|启用/禁用后台事件队列。|  
|`SCC_OPT_USERDATA`|任意值|指定要传递给 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 回调函数的用户值。|  
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|指示 IDE 当前是否支持取消操作。|  
|`SCC_OPT_NAMECHANGEPFN`|指向 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 回调函数的指针|设置指向名称更改回调函数的指针。|  
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|指示 IDE 是否允许通过源代码管理用户界面手动签出其文件 () 或是否必须仅通过源代码管理插件将其签出。|  
|`SCC_OPT_SHARESUBPROJ`|不适用|如果源代码管理插件允许 IDE 指定本地项目文件夹，则插件将返回 `SCC_I_SHARESUBPROJOK` 。|  
  
## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE  
 如果 `nOption` 为 `SCC_OPT_EVENTQUEUE` ，则 IDE 正在禁用 (或重新启用) 后台处理。 例如，在编译期间，IDE 可能会指示源代码管理插件停止任意类型的空闲处理。 编译完成后，它将重新启用后台处理，以使插件的事件队列保持最新。 对应于的 `SCC_OPT_EVENTQUEUE` 值 `nOption` ，有两个可能的值 `dwVal` ，即 `SCC_OPT_EQ_ENABLE` 和 `SCC_OPT_EQ_DISABLE` 。  
  
## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE  
 如果的值 `nOption` 为 `SCC_OPT_HASCANCELMODE` ，则 IDE 允许用户取消长时间的操作。 设置 `dwVal` 为 `SCC_OPT_HCM_NO` (默认) 指示 IDE 没有取消模式。 如果希望用户能够取消，则源代码管理插件必须提供其自己的 "取消" 按钮。 `SCC_OPT_HCM_YES` 指示 IDE 可以取消操作，因此 SCC 插件无需显示其自己的 "取消" 按钮。 如果 IDE 将设置 `dwVal` 为 `SCC_OPT_HCM_YES` ，则准备响应 `SCC_MSG_STATUS` 并 `DOCANCEL` 发送到 `lpTextOutProc` 回调函数的消息 (参阅 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)) 。 如果 IDE 未设置此变量，则该插件不应发送这两条消息。  
  
## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN  
 如果将 nOption 设置为 `SCC_OPT_NAMECHANGEPFN` ，并且源代码管理插件和 IDE 都允许这样做，则该插件可以在源代码管理操作期间实际重命名或移动文件。 `dwVal`将设置为[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)类型的函数指针。 在源代码管理操作期间，插件可以调用此函数，同时传递三个参数。 它们是使用完全限定路径)  (旧名称、新名称 (该文件的完全限定路径) 以及指向与 IDE 相关的信息的指针。 IDE 通过在设置为的情况下调用来发送此最后一个指针 `SccSetOption` `nOption` `SCC_OPT_USERDATA` ， `dwVal` 指向数据。 此函数的支持是可选的。 使用此功能的 VSSCI 插件必须将其函数指针和用户数据变量初始化为 `NULL` ，且不能调用重命名函数，除非已为其提供一个。 还应准备好保存它所提供的值，或者将其更改为响应对的新调用 `SccSetOption` 。 此操作不会在源代码管理命令操作的过程中发生，但可能发生在命令之间。  
  
## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY  
 如果将 nOption 设置为 `SCC_OPT_SCCCHECKOUTONLY` ，则 IDE 将指示当前打开的项目中的文件永远不会通过源代码管理系统的用户界面手动签出。 相反，应仅通过 IDE 控件下的源代码管理插件签出文件。 如果 `dwValue` 设置为 `SCC_OPT_SCO_NO` ，则表示文件应由插件正常处理，并可通过源代码管理 UI 签出。 如果 `dwValue` 设置为 `SCC_OPT_SCO_YES` ，则只允许插件签出文件，并且不应调用源代码管理系统的 UI。 这适用于以下情况： IDE 可能有 "伪文件"，只需通过 IDE 即可查看。  
  
## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ  
 如果 `nOption` 设置为 `SCC_OPT_SHARESUBPROJ` ，则 IDE 将测试源代码管理插件是否可以在从源代码管理添加文件时使用指定的本地文件夹。 `dwVal`在这种情况下，参数的值并不重要。 如果插件允许 IDE 指定本地目标文件夹，在调用 [SccAddFromScc](../extensibility/sccaddfromscc-function.md) 时，将从源代码管理中添加文件，则 `SCC_I_SHARESUBPROJOK` 调用函数时必须返回插件 `SccSetOption` 。 然后，IDE 使用该 `lplpFileNames` 函数的参数 `SccAddFromScc` 传入目标文件夹。 此插件使用目标文件夹将文件添加到源代码管理中。 如果在 `SCC_I_SHARESUBPROJOK` 设置该选项时插件未返回 `SCC_OPT_SHARESUBPROJ` ，IDE 将假定插件只能在当前的本地文件夹中添加文件。  
  
## <a name="see-also"></a>另请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)   
 [SccAddFromScc](../extensibility/sccaddfromscc-function.md)   
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)   
 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
