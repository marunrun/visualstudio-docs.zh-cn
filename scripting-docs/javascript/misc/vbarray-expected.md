---
title: 缺少 VBArray |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
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
ms.openlocfilehash: 5d1fabd8da6f825a266614a4a5c7fabd5c307130
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63005987"
---
# <a name="vbarray-expected"></a>缺少 VBArray
您提供了一个对象，不是 Visual Basic 的 safeArray，当一个期望值。  
  
```js
new VBArray(safeArray);  
```  
  
 VBArray 是只读的，不能直接创建。 SafeArray 参数是一个 VBArray 值，和之前，必须获取一个 VBArray 值传递给`VBArray`构造函数。 只有从现有的 ActiveX 或其他对象进行检索，才能获取该值。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 确保只能通过**VBArray**对象添加到**VBArray**构造函数。  
  
## <a name="see-also"></a>请参阅  
 [VBArray 对象](../../javascript/reference/vbarray-object-javascript.md)   
 [使用数组](../../javascript/advanced/using-arrays-javascript.md)