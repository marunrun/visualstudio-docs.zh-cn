---
title: 错误：TRANSACT-SQL 执行未经调试便已结束 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- FSharp
- VB
- CSharp
- C++
- SQL
ms.assetid: 7a4d4999-3973-4339-ba6a-f0d19bcb1d4a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cdfcaa42c55f87711b0889c6a67d1a4799b84fed
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65681078"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>错误：Transact-SQL 执行未经调试便已结束
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当尝试调试 Transact-SQL 或 SQLCLR 过程而调试器未从 SQL Server 接收调试消息时，会发生此错误。  
  
 这可能是由于网络问题或 SQL Server 上的问题造成的，但是可能性最大的原因是权限问题。  
  
 这涉及到两种帐户：  
  
- 应用程序帐户是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 运行时所用的用户帐户。  
  
- 连接帐户是用于建立到 SQL Server 的连接的标识。 这不一定是该连接使用 SQL 身份验证时 Visual Studio 运行所使用的标识。  
  
  SQL 调试要求应用程序帐户必须与连接帐户匹配或者是系统管理员。  
  
  如果正使用某个类似于 sa 的 SQL 登录，则该应用程序帐户在 SQL Server 上必须设置为系统管理员。 默认情况下，运行 SQL server 的计算机上的管理员是 SQL Server 系统管理员。  
  
  若要纠正此错误，可能需要：  
  
- 验证权限设置。 有关详细信息，请参阅[如何：设置 SQL Server 权限以进行调试](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)。  
  
- 如果设置正确，请确保 SQL 调试也正确。  
  
- 请咨询网络或数据库管理员。  
  
## <a name="see-also"></a>请参阅  
 [设置 SQL 调试](https://msdn.microsoft.com/3db09e68-edcc-42de-9c22-4e97cfd55ab3)   
 [如何：设置 SQL Server 权限以进行调试](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)   
 [远程调试](../debugger/remote-debugging.md)
