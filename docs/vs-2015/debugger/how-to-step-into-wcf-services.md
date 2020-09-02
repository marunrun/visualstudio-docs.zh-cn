---
title: 如何：单步执行 WCF 服务 | Microsoft Docs
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
- debugging, WCF
- WCF, debugging
ms.assetid: 9893ad01-54af-499f-85a6-9d1cfe6eb640
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 951d5f39fbf3929d094cc18de5fe108b46753b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176522"
---
# <a name="how-to-step-into-wcf-services"></a>如何：单步执行 WCF 服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] 中，可以单步执行 WCF 服务。 如果 WCF 服务与客户端位于同一 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中，则可以命中 WCF 服务内部的断点。  
  
 若要使单步执行正常运行，必须在 app.config 或 Web.config 文件中启用调试。 有关如何启用调试的信息以及有关单步执行 WCF 服务的限制，请参阅 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。  
  
### <a name="to-step-into-a-wcf-service"></a>单步执行 WCF 服务  
  
1. 创建一个同时包含 WCF 客户端和 WCF 服务项目的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案。  
  
2. 在解决方案资源管理器中，右键单击“WCF 客户端”项目，再单击“设为启动项目”。  
  
3. 在 app.config 或 web.config 文件中启用调试。 有关详细信息，请参阅 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。  
  
4. 在客户端项目中需要开始单步执行的位置设置断点。 通常情况下，断点设置在 WCF 服务调用之前。  
  
5. 运行到断点，然后开始单步执行。 调试程序将自动在服务中单步执行。  
  
## <a name="see-also"></a>另请参阅  
 [调试 WCF 服务](../debugger/debugging-wcf-services.md)   
 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)   
 [如何：调试自托管 WCF 服务](../debugger/how-to-debug-a-self-hosted-wcf-service.md)
