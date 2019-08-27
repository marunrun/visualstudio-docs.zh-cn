---
title: IActiveScriptProfilerControl5 Interface | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7fd0ce34-6ae3-428f-ba90-3e86a8a98ed0
caps.latest.revision: 2
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dacca8e8bf161b6f3a84dc216596673d5df8258c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992906"
---
# <a name="iactivescriptprofilercontrol5-interface"></a>IActiveScriptProfilerControl5 接口
提供的方法来枚举与脚本引擎关联的 GC 堆对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
interface IActiveScriptProfilerControl5 : IActiveScriptProfilerControl4  
```  
  
## <a name="methods"></a>方法  
 [IActiveScriptProfilerControl5::EnumHeap2 方法](../../winscript/reference/iactivescriptprofilercontrol5-enumheap2-method.md)  
 返回的接口 ([IActiveScriptProfilerHeapEnum 接口](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)) 可用于循环访问关联的脚本引擎的上下文中的 GC 堆对象。