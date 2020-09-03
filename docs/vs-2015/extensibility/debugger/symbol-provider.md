---
title: 符号提供程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6af1af9d2e178241fa8a5957e18c1a5333fa4b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178887"
---
# <a name="symbol-provider"></a>符号提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

表达式计算器实现必须访问语言编译器生成的符号调试信息，才能计算变量和表达式。 它通过使用符号提供程序 (SP) （也称为符号处理程序）的接口来实现此目的。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 使用程序数据库为托管代码和本机代码提供 Sp (PDB) 符号文件格式。 除非你的程序很难使用以自定义格式存储的符号，否则建议你使用提供的 Sp [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
## <a name="implementation-notes"></a>实现说明  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试引擎需要使用公共语言运行时 (CLR) 接口与 SPs 进行通信。 因此，将使用 Visual Studio 调试引擎的 SP 必须支持 CLR。 可以在 debugref.doc 中找到所有 CLR 调试接口的完整列表，该列表是的一部分 [!INCLUDE[winsdklong](../../includes/winsdklong-md.md)] 。  
  
 如果您的 SP 只使用您的自定义调试引擎，则可以根据调试引擎的需求，根据您的需要实现 SP。  
  
## <a name="see-also"></a>另请参阅  
 [调试器组件](../../extensibility/debugger/debugger-components.md)
