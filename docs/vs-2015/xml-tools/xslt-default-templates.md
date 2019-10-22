---
title: XSLT 默认模板 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 773dd34e-67d3-4997-8df9-b71e7f880d88
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5bb4351d6b95c7aee929274135454ecf7aa91574
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669327"
---
# <a name="xslt-default-templates"></a>XSLT 默认模板
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 XSLT 处理期间，如果在样式表中没有匹配的显式模板规则，则使用默认模板。 在 W3C XSLT 1.0 建议的第 5.8 节中定义了默认模板（也称为内置模板规则）。 默认模板允许 XSLT 处理器处理节点，即使没有与其匹配的显式模板规则也如此。 但是，因为没有在样式表中显式定义内置模板规则，所以可能导致意外的或混乱的 XSLT 转换结果。

 XSLT 调试器此时显示 XSLT 默认模板的代码。 当逐句通过 XSLT 转换时，如果使用默认模板，则调试器在窗口中显示默认模板。 这使您能够逐句通过默认模板的代码并且按照它的说明设置断点。

## <a name="see-also"></a>请参阅
 [调试 XSLT](../xml-tools/debugging-xslt.md)
