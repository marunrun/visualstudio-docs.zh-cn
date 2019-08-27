---
title: 错误：用户未能执行存储过程 sp_enable_sql_debug |Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e051cd594ee26a57fdbb7dcdc5bdad81f06cf771
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62850089"
---
# <a name="error-user-could-not-execute-stored-procedure-spenablesqldebug"></a>错误：用户无法执行存储过程 sp_enable_sql_debug

在服务器上未能执行存储过程 sp_enable_sql_debug。 这可能是由于：

- 连接问题。 需要有一个到服务器的稳定连接。

- 在服务器上缺少必要的权限。 若要在 SQL Server 2005 上调试，运行 Visual Studio 的帐户和用于连接 SQL Server 的帐户都必须是 sysadmin 角色的成员。 用于连接 SQL Server 的帐户要么是 Windows 用户帐户（如果您正在使用 Windows 身份验证），要么是具有用户 ID 和密码的帐户（如果您使用 SQL 身份验证）。

有关详细信息，请参阅[如何：设置 SQL Server 权限以进行调试](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)。

## <a name="see-also"></a>请参阅

- [如何：设置 SQL Server 权限以进行调试](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)
- [设置 SQL 调试](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))