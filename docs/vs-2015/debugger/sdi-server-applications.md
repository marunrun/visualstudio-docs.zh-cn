---
title: SDI 服务器应用程序 |Microsoft Docs
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
- SDI server applications
- SDI server applications, debugging
ms.assetid: 09713718-1376-4753-b119-26f36639693e
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1296c0f43d0409df0081861095c5ec068932bbc1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148152"
---
# <a name="sdi-server-applications"></a>SDI 服务器应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果调试的是 SDI 服务器应用程序，对于 C/C++、C# 或 Visual Basic 项目，必须在“项目属性页”对话框中的“命令行参数”属性中指定 `/Embedding` 或 `/Automation`   。  
  
 使用这些命令行参数，调试器可以像从容器中启动服务器应用程序一样启动它。 从程序管理器或文件管理器启动容器将导致容器使用在调试器中启动的服务器实例。  
  
## <a name="finding-the-command-line-arguments-property"></a>查找“命令行参数”属性  
 若要访问“项目属性页”对话框，请在解决方案资源管理器中右键单击项目，然后从快捷菜单中选择“属性”  。 若要找到“命令行参数”属性，请展开“配置属性”类别并单击“调试”页。  
  
## <a name="see-also"></a>请参阅  
 [调试 COM 和 ActiveX](../debugger/com-and-activex-debugging.md)   
 [如何：调试 COM 服务器](../debugger/how-to-debug-com-servers.md)
