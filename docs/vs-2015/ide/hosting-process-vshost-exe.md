---
title: 承载进程 (vshost.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- vshost.exe
- hosting process
ms.assetid: c6b9e2be-f18d-4d75-ac52-56d55784734b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a998246f514f13a575f6a7fef850f9f705f92553
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645535"
---
# <a name="hosting-process-vshostexe"></a>承载进程 (vshost.exe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

承载进程是 Visual Studio 中的功能，它改进了调试性能、启用了部分信任调试和设计时表达式计算。 承载进程文件的文件名中包含 vshost，位于项目的输出文件夹中。 有关详细信息，请参阅[调试和承载进程](../debugger/debugging-and-the-hosting-process.md)。

> [!NOTE]
> 承载进程文件 (.vshost.exe) 适用于 Visual Studio 并且不应直接运行或与应用程序一起部署。

## <a name="improved-debugging-performance"></a>改进的调试性能
 承载进程创建应用程序域并将调试器与应用程序关联起来。 执行这些任务会导致开始调试和开始运行应用程序之间出现明显时间延迟。 承载进程可帮助提高性能，方法是：在后台创建应用程序域并关联调试器，然后在运行应用程序之间保存应用程序域和调试器状态。 有关应用程序域的详细信息，请参阅[应用程序域](https://msdn.microsoft.com/library/113a8bbf-6875-4a72-a49d-ca2d92e19cc8)。

## <a name="partial-trust-debugging"></a>部分信任调试
 在“项目设计器”的[安全页](../ide/reference/security-page-project-designer.md)中，可将应用程序指定为部分信任应用程序。 调试部分信任应用程序需要对应用程序域进行特殊的初始化。 此初始化由承载进程处理。

## <a name="design-time-expression-evaluation"></a>设计时表达式求值
 借助设计时表达式计算，你可从“即时”窗口进行代码测试，而不必运行应用程序。 承载进程在设计时表达式计算期间执行此代码。 有关详细信息，请参阅[即时窗口](../ide/reference/immediate-window.md)。

## <a name="see-also"></a>请参阅
 [调试和宿主进程](../debugger/debugging-and-the-hosting-process.md)[如何：禁用宿主进程的](../ide/how-to-disable-the-hosting-process.md)[即时窗口](../ide/reference/immediate-window.md)[应用程序域](https://msdn.microsoft.com/library/113a8bbf-6875-4a72-a49d-ca2d92e19cc8)
