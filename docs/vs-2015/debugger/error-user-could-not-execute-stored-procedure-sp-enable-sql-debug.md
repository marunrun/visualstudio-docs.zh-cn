---
title: 错误：用户无法执行存储过程 sp_enable_sql_debug | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.sqlde_accessdenied
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 11957495-c238-4cc5-8937-e4026f5e10e1
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 759386728283d3d39219133e53668afe3259714a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697678"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>错误：用户无法执行存储过程 sp_enable_sql_debug
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在服务器上未能执行存储过程 sp_enable_sql_debug。 这可能是由于：  
  
- 连接问题。 需要有一个到服务器的稳定连接。  
  
- 在服务器上缺少必要的权限。 若要在 SQL Server 2005 上调试，运行 Visual Studio 的帐户和用于连接 SQL Server 的帐户都必须是 sysadmin 角色的成员。 用于连接 SQL Server 的帐户要么是 Windows 用户帐户（如果您正在使用 Windows 身份验证），要么是具有用户 ID 和密码的帐户（如果您使用 SQL 身份验证）。  
  
  有关详细信息，请参阅[如何：设置 SQL Server 调试权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)。  
  
## <a name="see-also"></a>另请参阅  
 [如何：设置用于调试的 SQL Server 权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [设置 SQL 调试](https://msdn.microsoft.com/3db09e68-edcc-42de-9c22-4e97cfd55ab3)
