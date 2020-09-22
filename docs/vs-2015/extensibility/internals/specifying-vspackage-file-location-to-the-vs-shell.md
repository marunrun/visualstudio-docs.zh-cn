---
title: 将 VSPackage 文件位置指定到 VS Shell |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c0662bfe22b4c78bb754bbac2fbfdd281a4a7bce
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840783"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>指定 VS Shell 的 VSPackage 文件位置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 必须能够找到用于加载 VSPackage 的程序集 DLL。 您可以通过多种方式找到该方法，如下表所述。  
  
|方法|说明|  
|------------|-----------------|  
|使用 CodeBase 注册表项。|基本代码键可用于指示 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 从任何完全限定的文件路径加载 VSPackage 程序集。 键的值应为 DLL 的文件路径。 这是 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 加载包程序集的最佳方式。 此方法有时称为 "基本代码/专用安装目录技术"。 在注册期间，基本代码的值通过类型的实例传递给注册属性类 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext> 。|  
|将 DLL 放置在 **PrivateAssemblies** 目录中。|将程序集放在目录的 **PrivateAssemblies** 子目录中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 系统会自动检测位于 **PrivateAssemblies** 中的程序集，但在 " **添加引用** " 对话框中看不到这些程序集。 **PrivateAssemblies**和**PublicAssemblies**之间的区别在于： **PublicAssemblies**中的程序集在 "**添加引用**" 对话框中进行枚举。 如果选择不使用 "基本代码/专用安装目录" 技术，则应安装到 **PrivateAssemblies** 目录中。|  
|使用具有强名称的程序集和程序集注册表项。|可以使用程序集键显式定向 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 到加载强名称的 VSPackage 程序集。 键的值应为程序集的强名称。|  
|将 DLL 放置在 **PublicAssemblies** 目录中。|最后，还可以将程序集放置在 **PublicAssemblies** 子目录中。 系统会自动检测位于 **PublicAssemblies** 中的程序集，这些程序集也会显示在中的 " **添加引用** " 对话框中 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。<br /><br /> 如果 VSPackage 的程序集包含旨在由其他 VSPackage 开发人员重新使用的托管组件，则只能将这些程序集放入 **PublicAssemblies** 目录中。 大多数程序集不满足此条件。|  
  
> [!NOTE]
> 为所有依赖程序集使用具有强名称的已签名程序集。 还应将这些程序集安装在自己的目录或全局程序集缓存 (GAC) 。 这可以防止与具有相同基文件名（称为弱名称绑定）的程序集发生冲突。
