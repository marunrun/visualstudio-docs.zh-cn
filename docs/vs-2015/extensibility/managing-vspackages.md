---
title: 管理 Vspackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b56ab490342cfbda9c16408aa0937abd80728c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194377"
---
# <a name="managing-vspackages"></a>管理 VSPackages
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在大多数情况下，你无需担心如何管理 Vspackage，因为项目和项模板会自动注册并加载包。 但是，在某些情况下，你可能需要更多地了解，才能管理包。  
  
## <a name="using-the-experimental-instance"></a>使用实验实例  
 若要了解有关实验实例的详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。  
  
## <a name="registering-and-unregistering-vspackages"></a>注册和注销 VSPackage  
 若要了解如何注册和注销 Vspackage 和其他类型的扩展，请参阅 [注册和注销 vspackage](../extensibility/registering-and-unregistering-vspackages.md)。  
  
## <a name="loading-a-vspackage"></a>加载 VSPackage  
 当启用特定 CMDUICONTEXT GUID 时，可以将 Vspackage 设置为 autoload。 有关详细信息，请参阅 [加载 vspackage](../extensibility/loading-vspackages.md)。  
  
## <a name="using-asyncpackage-to-load-vspackages-in-the-background"></a>使用 AsyncPackage 在后台加载 Vspackage  
 AsyncPackage 类可在后台线程上启用包加载，以便在 Visual Studio 中实现更好的 UI 响应能力。 有关详细信息，请参阅 [如何：使用 AsyncPackage 在后台加载 vspackage](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)。  
  
## <a name="rule-based-ui-context-for-extensions"></a>用于扩展的基于规则的 UI 上下文  
 基于规则的 UI 上下文允许扩展创作者定义激活 UI 上下文以及 Vspackage 加载关联的精确条件。 有关详细信息，请参阅 [如何：将基于规则的 UI 上下文用于 Visual Studio 扩展](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)。  
  
## <a name="troubleshooting-vspackages"></a>VSPackages 故障排除  
 了解故障排除 Vspackage 的技术，这些技术无法加载或遇到错误： [疑难解答 vspackage](../extensibility/troubleshooting-vspackages.md)  
  
## <a name="see-also"></a>另请参阅  
 [VSPackages](../extensibility/internals/vspackages.md)
