---
title: 错误：SQL 可以&#39;t 不到 Ssdebugps |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.sqlde_cant_find_ssdebugps
dev_langs:
- FSharp
- VB
- CSharp
- C++
- SQL
ms.assetid: 596425c8-14c7-4c05-8823-e1c52f420f5e
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 25462a99bd3e773f03af3918a9e25d11ed006c1c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185219"
---
# <a name="error-sql-can39t-find-ssdebugps"></a>错误：SQL 可以&#39;t 不到 Ssdebugps
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SSDEBUGPS.dll 为 SQL Server Debugging Host 组件。  
  
 此错误在尝试开始调试时发生，指示指定的文件在 [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] 计算机上不存在。 可能的原因是从未运行远程调试安装，或是由于某种原因删除了此文件。  
  
 有两种方法可以纠正此错误：重新运行远程调试安装，以及将该文件复制到 [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] 计算机上。  
  
 若要重新运行远程调试安装，请按照的说明[远程调试](../debugger/remote-debugging.md)。  
  
 如果可以找到 ssdebugps.dll 的某个副本，则可以将其复制到 [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] 计算机上。 如果存在，该文件会位于目录 \Program Files\ Common Files\Microsoft Shared\SQL Debugging 中。 你可能会发现它在另一台[!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)]的计算机上的计算机或[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]安装。  
  
### <a name="to-copy-ssdebugpsdll-onto-the-sql-server-2005-machine"></a>将 SSDEBUGPS.dll 复制到 SQL Server 2005 计算机上  
  
1. 将该文件复制到 [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] 计算机上具有相同名称和路径的目录中。  
  
2. 通过打开“命令提示符”并运行下面的命令来注册该文件  ：  
  
    ```  
    regsvr32 ssdebugps.dll  
    ```
