---
title: 如何：单步执行 WCF 服务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, debugging
ms.assetid: 9893ad01-54af-499f-85a6-9d1cfe6eb640
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c405b4fcca91f8deddce4d65c8a4155b90af49e0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732602"
---
# <a name="how-to-step-into-wcf-services"></a>如何：单步执行 WCF 服务
在 [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] 中，可以单步执行 WCF 服务。 如果 WCF 服务与客户端位于同一 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 解决方案中，则可以命中 WCF 服务内部的断点。

 若要使单步执行正常运行，必须在 app.config 或 Web.config 文件中启用调试。 有关如何启用调试的信息以及有关单步执行 WCF 服务的限制，请参阅 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。

### <a name="to-step-into-a-wcf-service"></a>单步执行 WCF 服务

1. 创建一个同时包含 WCF 客户端和 WCF 服务项目的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 解决方案。

2. 在解决方案资源管理器中，右键单击“WCF 客户端”项目，再单击“设为启动项目”。

3. 在 app.config 或 web.config 文件中启用调试。 有关详细信息，请参阅 [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)。

4. 在客户端项目中需要开始单步执行的位置设置断点。 通常情况下，断点设置在 WCF 服务调用之前。

5. 运行到断点，然后开始单步执行。 调试程序将自动在服务中单步执行。

## <a name="see-also"></a>请参阅
- [调试 WCF 服务](../debugger/debugging-wcf-services.md)
- [WCF 调试的限制](../debugger/limitations-on-wcf-debugging.md)
- [如何：调试自托管 WCF 服务](../debugger/how-to-debug-a-self-hosted-wcf-service.md)