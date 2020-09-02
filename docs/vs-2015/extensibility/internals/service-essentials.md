---
title: 服务基础 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696070"
---
# <a name="service-essentials"></a>服务基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

服务是两个 Vspackage 之间的协定。 一个 VSPackage 为其他要使用的 VSPackage 提供一组特定的接口。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 本身是 Vspackage 的集合，可向其他 Vspackage 提供服务。  
  
 例如，你可以使用 SVsActivityLog 服务来获取 IVsActivityLog 接口，该接口可用于写入活动日志。 有关详细信息，请参阅 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 还提供一些未注册的内置服务。 Vspackage 可以通过提供服务重写来替换内置或其他服务。 对于任何服务，只允许一个服务替代。  
  
 服务没有可发现性。 因此，你必须知道要使用的服务 (SID) 的服务标识符，并且必须知道它提供了哪些接口。 服务的参考文档提供了此信息。  
  
- 提供服务的 Vspackage 称为服务提供商。  
  
- 向其他 Vspackage 提供的服务称为全局服务。  
  
- 仅可用于实现它们的 VSPackage 或为其创建的任何对象的服务称为 "本地服务"。  
  
- 替换内置服务或其他包提供的服务的服务称为服务重写。  
  
- 服务或服务重写是按需加载的，也就是说，当另一个 VSPackage 请求服务提供程序时，将加载该服务提供程序。  
  
- 若要支持按需加载，服务提供商可向注册其全局服务 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 有关详细信息，请参阅 [注册服务](../../misc/registering-services.md)。  
  
- 获取服务后，使用 [QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) (非托管代码) 或强制转换 (托管代码) 以获取所需的接口，例如：  
  
    ```vb  
    TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)  
    ```  
  
    ```csharp  
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
  
    ```  
  
- 托管代码按其类型引用服务，而非托管代码通过其 GUID 来引用服务。  
  
- [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]加载 VSPackage 时，它会将服务提供程序传递到 VSPackage，以便 VSPackage 访问全局服务。 这称为 "选址" VSPackage。  
  
- Vspackage 可以是其创建的对象的服务提供商。 例如，窗体可能会将颜色服务请求发送到其框架，这可能会将请求传递给 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
- 深度嵌套或根本没有放置的托管对象可能会调用 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 以直接访问全局服务。 有关详细信息，请参阅 how [to： Use GetGlobalService](../../misc/how-to-use-getglobalservice.md)。  
  
## <a name="see-also"></a>另请参阅  
 [可用服务列表](../../extensibility/internals/list-of-available-services.md)   
 [使用和提供服务](../../extensibility/using-and-providing-services.md)   
 [强制转换和类型转换](https://msdn.microsoft.com/library/568df58a-d292-4b55-93ba-601578722878)   
 [强制转换](https://msdn.microsoft.com/library/3dbeb06e-2f4b-4693-832d-624bc8ec95de)
