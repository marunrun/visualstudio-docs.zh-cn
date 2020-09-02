---
title: 可视化工具安全注意事项 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- visualizers, security
- security [Visual Studio], visualizers
ms.assetid: cdd86bd5-b729-409b-a7c6-374efa091eb1
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 51c79c34520c36e51599d4d6135784f493673b62
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146464"
---
# <a name="visualizer-security-considerations"></a>可视化工具安全注意事项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编写可视化工具伴有可能的安全威胁。 目前尚未发现利用这些潜在威胁的攻击，但是开发人员应该密切关注此类攻击并采取此处所描述的相应安全预防措施，以防止在将来受到攻击。  
  
 调试器可视化工具要求比部分信任的应用程序允许的特权更大的特权。 在部分信任的代码中停止时，可视化工具不会加载。 若要使用可视化工具进行调试，必须运行完全信任的代码。  
  
## <a name="possible-malicious-debuggee-component"></a>可能的恶意调试对象组件  
 可视化工具至少由两个类组成：一个位于调试器端，另一个位于调试对象端。 可视化工具通常部署在放置在特殊目录中的不同程序集中，但也可以从调试对象加载它们。 此时，调试器将代码从调试对象中取出并在完全信任的情况下在调试器内部运行代码。  
  
 当调试对象不完全受信任时，在完全信任的情况下运行调试对象端代码会有问题。 如果可视化工具尝试将一个部分信任的程序集从调试对象加载到调试器中，则 Visual Studio 将终止此可视化工具。  
  
 然而，微小的漏洞仍然存在。 调试对象端可以与从另一个源（不是调试对象）加载的调试器端相关联。 调试对象端然后可以通知受信任的调试器端代表它执行操作。 例如，如果受信任的调试器端类公开一个“删除此文件”机制，则当用户调用其可视化工具时，部分信任的调试对象就会调用此机制。  
  
 若要减轻此漏洞的影响，请注意可视化工具公开的接口。  
  
## <a name="see-also"></a>另请参阅  
 [可视化工具体系结构](../debugger/visualizer-architecture.md)   
 [如何：编写可视化工具](../debugger/how-to-write-a-visualizer.md)   
 [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)   
 [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
