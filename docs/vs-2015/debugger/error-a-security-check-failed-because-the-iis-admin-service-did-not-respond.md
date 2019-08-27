---
title: 错误：安全检查失败，因为 IIS 管理服务未响应 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.iis_not_responding
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 6060e94e-71dc-49f2-bb59-2584216eadbf
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65eb724d14123292a0694623bf46859f8a3966f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197091"
---
# <a name="error-a-security-check-failed-because-the-iis-admin-service-did-not-respond"></a>错误：安全检查失败，因为 IIS 管理服务没有响应
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当 IIS 管理服务没有响应时，会发生此错误。 这通常表示 IIS 的安装有问题。 首先，请使用“管理工具”中的“服务”工具验证该服务是否正在运行   。  
  
### <a name="to-correct-this-error"></a>更正此错误  
  
- 使用“添加或删除程序”控制面板重新安装 IIS  。  
  
- 或  
  
- 使用控制面板中的 “添加/删除程序” 从计算机中删除 IIS。 如果已移除 IIS，但是仍存在问题，请检查注册表，并确保下面的项不再存在：  
  
    ```  
    HKEY_CLASSES_ROOT\CLSID\{A9E69610-B80D-11D0-B9B9-00A0C922E750}  
    ```  
  
     或  
  
- 使用“管理工具”控制面板禁用 IIS 管理服务。 这将在您的计算机上禁用 IIS。  
  
     执行这三个步骤中的任一步骤后，重新启动计算机。  
  
     有关其他信息，请参见 IIS 文档。  
  
## <a name="see-also"></a>请参阅  
 [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
