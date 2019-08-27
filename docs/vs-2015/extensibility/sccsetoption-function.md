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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68143745"
---
# <a name="sccsetoption-function"></a>SccSetOption 函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此函数设置控制的源代码管理插件行为的选项。  
  
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
 [in]源控制插件上下文结构。  
  
 nOption  
 [in]正在设置的选项。  
  
 dwVal  
 [in]选项的设置。  
  
## <a name="return-value"></a>返回值  
 此函数的源控制插件实现应返回以下值之一：  
  
|值|描述|  
|-----------|-----------------|  
|SCC_OK|已成功设置的选项。|  
|SCC_I_SHARESUBPROJOK|如果`nOption`已`SCC_OPT_SHARESUBPROJ`和源代码管理插件允许 IDE 以将目标文件夹设置。|  
|SCC_E_OPNOTSUPPORTED|该选项不设置，并且不应依赖。|  
  
## <a name="remarks"></a>备注  
 IDE 将调用此函数可控制行为的源代码管理插件。 第一个参数， `nOption`，指示第二个，，正在设置的值`dwVal`，指示要执行的操作具有此值。 该插件将存储此信息与相关联`pvContext``,`以便 IDE 必须调用后调用此函数[SccInitialize](../extensibility/sccinitialize-function.md) (但不是一定是在每次调用后[SccOpenProject](../extensibility/sccopenproject-function.md))。  
  
 选项及其值的摘要：  
  
|`nOption`|`dwValue`|描述|  
|---------------|---------------|-----------------|  
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|启用/禁用背景事件队列。|  
|`SCC_OPT_USERDATA`|任意值|指定要传递给的用户值[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)回调函数。|  
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|指示是否在 IDE 目前支持取消操作。|  
|`SCC_OPT_NAMECHANGEPFN`|指向[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)回调函数|设置的名称更改回调函数的指针。|  
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|指示 IDE 允许带其文件 （通过源代码管理用户界面） 手动检查，或是否它们必须先签出只能通过源代码管理插件。|  
|`SCC_OPT_SHARESUBPROJ`|不可用|如果源代码管理插件允许 IDE 以指定的本地项目文件夹，该插件返回`SCC_I_SHARESUBPROJOK`。|  
  
## <a name="sccopteventqueue"></a>SCC_OPT_EVENTQUEUE  
 如果`nOption`是`SCC_OPT_EVENTQUEUE`，禁用 （或重新启用） 在 IDE 后台处理。 例如，在编译期间 IDE 可能会指示源代码管理插件，以停止上空闲处理的任何类型。 在编译后它会重新启用后台处理，以保持最新的即插即用接事件队列。 对应于`SCC_OPT_EVENTQUEUE`的值`nOption`，有两个可能值为`dwVal`，即`SCC_OPT_EQ_ENABLE`和`SCC_OPT_EQ_DISABLE`。  
  
## <a name="sccopthascancelmode"></a>SCC_OPT_HASCANCELMODE  
 如果为值`nOption`是`SCC_OPT_HASCANCELMODE`，IDE 允许用户取消长时间操作。 设置`dwVal`到`SCC_OPT_HCM_NO`（默认值） 指示 IDE 具有无取消模式。 如果希望用户能够取消，源代码管理插件必须提供自己的取消按钮。 `SCC_OPT_HCM_YES` 指示 IDE 提供了取消操作，因此 SCC 插件不需要以显示自己的取消按钮的功能。 如果 IDE 设置`dwVal`到`SCC_OPT_HCM_YES`，它已准备好应对`SCC_MSG_STATUS`并`DOCANCEL`消息发送到`lpTextOutProc`回调函数 (请参阅[LPTEXTOUTPROC](../extensibility/lptextoutproc.md))。 如果 IDE 未设置此变量，该插件应发送这两条消息。  
  
## <a name="sccoptnamechangepfn"></a>SCC_OPT_NAMECHANGEPFN  
 如果 nOption 设置为`SCC_OPT_NAMECHANGEPFN`，和这两个源代码管理插件和 IDE 允许它，该插件可以实际重命名或移动文件在源代码管理操作过程。 `dwVal`将设置为类型的函数指针[OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)。 在源代码管理操作，该插件可以调用此函数，在三个参数中传递。 这些是文件，该文件中和一个指向具有与 IDE 的相关性的信息的新名称 （包含完全限定路径） 的旧名称 （包含完全限定路径）。 在此最后一个指针中发送通过调用的 IDE`SccSetOption`与`nOption`设置为`SCC_OPT_USERDATA`，使用`dwVal`指向数据。 对此函数的支持是可选的。 VSSCI 插件-可使用此功能必须将初始化为其函数指针和用户数据变量`NULL`，并且它必须不会调用重命名函数，除非它已被授予一个。 它应还准备用于保存为其指定的值，或将其更改以响应对的新调用`SccSetOption`。 此操作不会中间源代码管理命令操作，但它可能会发生在命令之间。  
  
## <a name="sccoptscccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY  
 如果设置为 nOption `SCC_OPT_SCCCHECKOUTONLY`，IDE 指示，当前打开的项目中的文件还是应该永远不会检查手动通过源代码管理系统的用户界面。 相反，应将文件签只能通过源代码管理插件 IDE 控制下。 如果`dwValue`设置为`SCC_OPT_SCO_NO`，这意味着文件应通常被视为该插件，可以通过源代码管理 UI 签出。 如果`dwValue`设置为`SCC_OPT_SCO_YES`，然后仅插件允许签出文件，并且不应调用的源控制系统 UI。 这是用于 IDE 可能会有"伪 files"有意义的签出只通过 IDE 的情况。  
  
## <a name="sccoptsharesubproj"></a>SCC_OPT_SHARESUBPROJ  
 如果`nOption`设置为`SCC_OPT_SHARESUBPROJ`，IDE 测试是否从源代码管理添加文件时，源代码管理插件可以使用指定的本地文件夹。 值`dwVal`参数在这种情况下并不重要。 如果该插件允许 IDE 以指定本地目标文件夹的文件源中将其添加控制何时[SccAddFromScc](../extensibility/sccaddfromscc-function.md)调用，则该插件必须返回`SCC_I_SHARESUBPROJOK`时`SccSetOption`函数调用。 然后使用 IDE`lplpFileNames`参数的`SccAddFromScc`函数传递目标文件夹中。 该插件使用该目标文件夹将添加从源代码管理中的文件。 如果未返回该插件`SCC_I_SHARESUBPROJOK`时`SCC_OPT_SHARESUBPROJ`选项设置，IDE 会假定该插件是能够将文件添加仅在当前的本地文件夹中。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)   
 [SccInitialize](../extensibility/sccinitialize-function.md)   
 [SccOpenProject](../extensibility/sccopenproject-function.md)   
 [SccAddFromScc](../extensibility/sccaddfromscc-function.md)   
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)   
 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
