---
title: 错误：远程计算机未显示在“远程连接”对话框中 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 5fd98a5b-2cf3-4438-8b0f-6f1a742a62ce
caps.latest.revision: 5
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a97211c1fa86123a2a7a65f2ff86b0cecac957dc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697325"
---
# <a name="error-remote-machine-does-not-appear-in-a-remote-connections-dialog"></a>错误：远程计算机未显示在“远程连接”对话框中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果远程计算机未显示在“远程连接”对话框中，请检查以下常见原因。  
  
 如果你使用托管的兼容模式，请检查的 Visual Studio 2010 文档： [远程调试疑难解答 - Visual Studio 2010](https://msdn.microsoft.com/library/2ys11ead\(v=vs.100\).aspx) 。  
  
### <a name="common-causes-for-this-error"></a>导致此错误的常见原因  
  
- 远程计算机正在位于不同子网中的计算机上运行。 若要解决此问题，在限定符对话框中手动键入计算机名称或 IP 地址  
  
- 远程调试器未在远程计算机上运行。 若要解决此问题，启动远程调试器。  
  
- 防火墙正在阻止 Visual Studio 和远程计算机之间的通信。 若要解决此问题，请将防火墙配置为允许 Visual Studio 和远程调试器 (msvsmon) 进行通信。  
  
- 防病毒软件正在阻止 Visual Studio 和远程计算机之间的通信。 若要解决此问题，请将防病毒软件配置为允许 Visual Studio 和远程调试器 (msvsmon) 进行通信。  
  
## <a name="see-also"></a>另请参阅  
 [在设备上安装远程工具](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)
