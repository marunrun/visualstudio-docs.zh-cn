---
title: 应为 VBArray |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: error-reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5013
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: f2998d7d-13a4-4bbe-b872-3ff3316551e4
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 09ab257e6c473e2747a24559200e7b1f432d5687
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815274"
---
# <a name="vbarray-expected"></a>缺少 VBArray
提供的对象不是 Visual Basic 的 safeArray （如果需要）。  
  
```js
new VBArray(safeArray);  
```  
  
 VBArray 是只读的，不能直接创建。 SafeArray 参数是 VBArray 值，必须先获取 VBArray 值，然后才能将其传递到 `VBArray` 构造函数。 只有从现有的 ActiveX 或其他对象进行检索，才能获取该值。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保仅将**VBArray**对象传递给**VBArray**构造函数。  
  
## <a name="see-also"></a>请参阅  
 [VBArray 对象](../../javascript/reference/vbarray-object-javascript.md)   
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)