---
title: VsgDbg 类 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 6722263c-ccef-40c7-a0ae-87a863fbab00
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 053647d48324f056148375bae9268b997ba8721f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145693"
---
# <a name="vsgdbg-class"></a>VsgDbg 类
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示一个接口，用于以编程方式控制图形诊断的应用内组件。  
  
## <a name="syntax"></a>语法  
  
```cpp  
class VsgDbg;  
```  
  
## <a name="members"></a>成员  
 `VsgDbg` 类支持以下成员。  
  
### <a name="public-constructors"></a>公共构造函数  
  
|“属性”|描述|  
|----------|-----------------|  
|[VsgDbg::VsgDbg（构造函数）](../debugger/vsgdbg-vsgdbg-constructor.md)|构造 `VsgDbg` 类的实例，还可以选择准备图形诊断的应用内组件，以主动捕获和记录图形信息。|  
|[VsgDbg::~VsgDbg（析构函数）](../debugger/vsgdbg-tilde-vsgdbg-destructor.md)|销毁 `VsgDbg` 类的实例。|  
  
### <a name="public-methods"></a>公共方法  
  
|“属性”|描述|  
|----------|-----------------|  
|[AddMessage](../debugger/addmessage.md)|将自定义消息添加到图形诊断 HUD（提醒显示）。|  
|[BeginCapture](../debugger/begincapture.md)|开始一个捕获间隔，该间隔将以 `EndCapture` 结束。|  
|[CaptureCurrentFrame](../debugger/capturecurrentframe.md)|将当前帧的剩余部分捕获到图形日志文件。|  
|[复制（编程捕获）](../debugger/copy-programmatic-capture.md)|将活动图形日志 (.vsglog) 文件的内容复制到新文件。|  
|[EndCapture](../debugger/endcapture.md)|结束以 `BeginCapture` 开始的捕获时间间隔。|  
|[Init](../debugger/init.md)|准备图形诊断的应用内组件，以主动捕获和记录图形信息。|  
|[ToggleHUD](../debugger/togglehud.md)|打开或关闭图形诊断的 HUD 覆盖。|  
|[UnInit](../debugger/uninit.md)|完成图形日志文件，将其关闭，并且在应用主动记录图形信息时释放已使用的资源。|  
  
## <a name="remarks"></a>备注  
 `VsgDbg` 类表示一个接口，可用于以编程方式控制图形诊断功能。 即使不主动捕获和记录图形信息，也可以使用某些功能，其中包括 `AddMessage` 成员函数和 `ToggleHUD` 成员函数。 其他成员函数要么准备图形诊断的应用内组件以启动或停止图形信息的主动捕获，要么必须在应用主动捕获图形信息并将其记录到图形日志文件时被调用。
