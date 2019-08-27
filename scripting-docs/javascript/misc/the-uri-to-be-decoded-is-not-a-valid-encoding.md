---
title: 要解码的 URI 不有效编码 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5025
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 029e0790-ffd1-496d-8700-3b3dbac1b6fd
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8fd8add72d016bc3f2e815f41c29c735505c8817
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63006216"
---
# <a name="the-uri-to-be-decoded-is-not-a-valid-encoding"></a>要解码的 URI 不是有效编码
你试图解码格式不正确的 URI （统一资源标识符）。 Uri 具有特殊的语法;大多数非字母数字字符必须进行编码，才可以在 URI 中使用。 可以使用`encodeURI`并`encodeURIComponent`方法来创建一个 URI，从正常[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]字符串。  
  
 完整的 URI 组成一系列组件和分隔符。 常规形式为：  
  
```JavaScript  
<Scheme>:<first>/<second>;<third>?<fourth>  
```  
  
 在尖括号中的名称表示组件，并":"，"/"，";"和"？"是保留的字符用作分隔符。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 请确保要解码有效的 Uri。 您不能进行解码正常[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)]字符串，因为它们可能包含无效字符。  
  
## <a name="see-also"></a>请参阅  
 [decodeURI 函数](../../javascript/reference/decodeuri-function-javascript.md)   
 [decodeURIComponent 函数](../../javascript/reference/decodeuricomponent-function-javascript.md)