---
title: 安全问题 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb6209882a7a71a68728299064edcc13afabff35
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704423"
---
# <a name="security-issues"></a>安全性问题
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

若要调试使用 Visual Studio 的程序，所需的唯一权限是相同的开发人员需要运行该程序。 这包括大多数情况下 （涉及其他服务，如 Internet 信息服务，某些情况下可能需要更高级别的权限） 的远程调试。  
  
 在 Visual Studio 运行时，进程调试管理器 (PDM) 在本地计算机上跟踪调试进程。 远程，由开发人员处理远程调试，使 PDM 启动一个名为 msvsmon.exe 程序。 （请注意 msvsmon.exe 不是一个服务，必须手动启动，以启用该计算机上远程调试。）当 Visual Studio （或 msvsmon.exe） 没有运行时，没有进程会跟踪以进行调试。  
  
 这意味着开发人员可以调试他或她开始使用任何特殊权限的程序。 开发人员甚至可以调试该其他人是否相同的安全组的成员由其他人启动的进程。 若要启用远程调试，因此需要就仅复制所需文件复制到远程计算机并启动 msvsmon.exe (请参阅[设置 Up the Remote Tools 在设备上](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)的更多详细信息)。  
  
## <a name="see-also"></a>请参阅  
 [调试任务](../../extensibility/debugger/debugging-tasks.md)   
 [进程调试管理器](../../extensibility/debugger/process-debug-manager.md)   
 [在设备上安装远程工具](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)
