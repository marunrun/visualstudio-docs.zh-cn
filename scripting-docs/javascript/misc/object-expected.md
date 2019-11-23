---
title: 应为对象 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5007
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 5d88c93d-e5b5-4b11-9bb5-bf1a5e41ccc3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1611596d844d43ef72663154dc48791830dfe29f
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573724"
---
# <a name="object-expected"></a>缺少对象
你尝试调用了 `Object` 类型以外的对象上的方法或属性，或在需要 `Object` 时传递了 `Object` 类型以外的自变量。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 仅调用类型为 `Object` 的对象上的方法或属性。  
  
- 如果非对象参数发生错误，则传递类型为 `Object` 的对象。  
  
- 检查是否正在调用未定义的或 null 引用而不是类型为 `Object` 的对象。  
  
     例如，如果以下代码的 myVar 上出现此错误：  
  
    ```JavaScript  
    var str = myVar.toString();  
    ```  
  
     可改用以下代码：  
  
    ```JavaScript  
    if (myVar) {  
        var str = myVar.toString();  
    }  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [对象对象](../../javascript/reference/object-object-javascript.md)   
 [对象和数组](../../javascript/objects-and-arrays-javascript.md)