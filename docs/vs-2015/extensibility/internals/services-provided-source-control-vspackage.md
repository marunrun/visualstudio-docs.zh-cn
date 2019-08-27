---
title: 提供的服务 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 750710cdc381573f8aa6fd064e1fc980030cf359
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202704"
---
# <a name="services-provided-source-control-vspackage"></a>提供的服务（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

服务是通过该功能被共享之间的 Visual Studio 集成的开发环境 (IDE) 和其已安装的 Vspackage 以及 Vspackage 之间的主要机制。 服务和 Visual Studio IDE 中的其重要性的详细说明，请参阅[使用和提供服务](../../extensibility/using-and-providing-services.md)。  
  
## <a name="the-source-control-service"></a>源代码管理服务  
 Visual Studio 提供了两个层的服务、 IDE 级别服务和包级别服务。 Visual Studio IDE 以本机方式提供 IDE 级别服务。 源代码管理包使用其中一些服务。 源代码管理包作为 VSPackage 通过提供其自己的专用源代码管理服务共享其源代码管理功能。 源代码管理包封装实现的协定可以由 Visual Studio IDE 的窗体中的源控件相关接口集。  
  
## <a name="see-also"></a>请参阅  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)
