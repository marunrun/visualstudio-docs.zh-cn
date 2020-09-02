---
title: ToggleHUD | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 87c2571926b92e59ae03e5e988bbf535474dc6d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68144575"
---
# <a name="togglehud"></a>ToggleHUD
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

打开或关闭图形诊断的 HUD（平视显示）覆盖。  
  
## <a name="syntax"></a>语法  
  
```cpp  
void ToggleHUD();  
```  
  
## <a name="remarks"></a>备注  
 图像诊断 HUD 显示在正在图形诊断下运行的应用的左上角。 它显示有关此应用和图形信息捕获的运行时信息，以及通过调用 [AddMessage](../debugger/addmessage.md) 成员函数添加的消息。  
  
 若要切换 HUD，不必主动捕获图形信息 - 也就是说，它可通过 `VsgDbg` 类的实例开关，但首先不必调用 [Init](../debugger/init.md) 成员函数。
