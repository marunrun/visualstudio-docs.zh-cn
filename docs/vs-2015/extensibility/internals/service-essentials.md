---
title: 服务 Essentials |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 407dda2f203b7be20b19c0e296caa9ce1c95b32c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696070"
---
# <a name="service-essentials"></a>服务基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

服务是两个 Vspackage 之间的协定。 一个 VSPackage 提供一组特定的另一个 VSPackage 来使用的接口。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 本身就是向其他 Vspackage 提供服务的 Vspackage 的集合。  
  
 例如，SVsActivityLog 服务可用于获取 IVsActivityLog 接口，它可用于写入活动日志。 有关详细信息，请参阅[如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 此外提供了一些内置的服务未注册。 Vspackage 可以通过提供服务重写替换内置或其他服务。 只有一个服务重写被允许的任何服务。  
  
 服务的任何可发现性。 因此，您必须知道服务标识符 (SID) 的一项服务，你想要使用，并且您必须知道它提供了哪些接口。 该服务的参考文档提供了此信息。  
  
- 提供服务的 Vspackage 称为服务提供商。  
  
- 提供给其他 Vspackage 的服务称为全局服务。  
  
- 仅适用于 VSPackage 实现它们，或到它创建任何对象，称为本地服务的服务。  
  
- 替换内置的服务或由其他包，提供服务的服务称为服务重写。  
  
- 按需加载服务或服务重写，它提供的服务请求的另一个 VSPackage 时，它是加载的服务提供程序。  
  
- 若要支持按需加载，服务提供程序注册其全球服务和[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 有关详细信息，请参阅[注册服务](../../misc/registering-services.md)。  
  
- 获取服务后，使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) （非托管代码） 或强制转换 （托管代码） 来获取所需的接口，例如：  
  
    ```vb  
    TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)  
    ```  
  
    ```csharp  
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
  
    ```  
  
- 托管的代码引用由其类型的服务，而非托管的代码引用的服务的 GUID。  
  
- 当[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]VSPackage 的加载，将其传递服务提供商到 VSPackage 以使 VSPackage 能够访问全球服务。 这称为"选址"VSPackage。  
  
- Vspackage 可以是服务提供商为他们创建的对象。 例如，窗体可能会将颜色服务的请求发送到其帧中，可能会向其传递请求[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
- 深度嵌套，或根本没有就位的托管的对象可以调用<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>直接访问全球服务。 有关详细信息，请参阅[如何：使用 GetGlobalService](../../misc/how-to-use-getglobalservice.md)。  
  
## <a name="see-also"></a>请参阅  
 [可用服务列表](../../extensibility/internals/list-of-available-services.md)   
 [使用并提供服务](../../extensibility/using-and-providing-services.md)   
 [强制转换和类型转换](https://msdn.microsoft.com/library/568df58a-d292-4b55-93ba-601578722878)   
 [强制转换](https://msdn.microsoft.com/library/3dbeb06e-2f4b-4693-832d-624bc8ec95de)
