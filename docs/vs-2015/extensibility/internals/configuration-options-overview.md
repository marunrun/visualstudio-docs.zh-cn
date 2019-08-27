---
title: 配置选项概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations
- configuration options, about configuration options
ms.assetid: f4ad4dd3-b39e-42df-ad89-d403cdf24a2b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b37d93adbd2accb7a12fb176ab15aafc6914190
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441512"
---
# <a name="configuration-options-overview"></a>配置选项概述
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

中的项目[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]可以支持多个可以生成、 调试、 运行，和/或已部署的配置。 配置是使用属性、 通常编译器开关和文件位置的命名集所述的生成类型。 默认情况下，新的解决方案包含两个配置，调试和发布。 可以使用其默认设置，或修改以满足您特定的解决方案和/或项目要求应用这些配置。 某些包可以生成两种方式： 作为一个 ActiveX 编辑器，或作为就地组件。 项目不需要支持多个配置，但是。 如果没有可用的只有一个配置，则该配置映射到的所有解决方案配置。  
  
 配置通常由两个部分-配置名称 （如调试或发布） 和平台设置。 配置的平台名称标识的配置目标，例如 API 设置的环境或操作系统平台。 用户的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]不能创建一个平台中; 它们必须从选项中选择 VSPackage 允许的项目。 当用户安装 VSPackage，在包开发过程中创建的交付平台，可能会出现任何所需的平台名称基于由包创建者设置任何条件。 然后，用户可以选择从实例化的属性页时可用于通过 VSPackage 的平台列表。  
  
 平台名称是可选的因为并非所有的项目支持的平台的概念。 时配置缺少平台名称，会在 UI 中显示字符串"n/A"。  
  
 每个解决方案都具有自己的一组的配置，其中只有一个可以处于活动状态一次。 解决方案配置是从每个项目的多个配置的一组。 "不能超过"的要求是由于要从解决方案配置中排除项目的选项。 用户可以创建自己的自定义解决方案配置。  
  
 下表说明了一个项目的典型配置设置。 行标记为配置名称和平台名称的列。  
  
|配置名称|平台-Win32|平台-Win64|  
|------------------------|----------------------|----------------------|  
|调试|\<调试 Win32 设置 >|\<调试 Win64 设置 >|  
|Release|\<发布 Win32 设置 >|\<发布 Win64 设置 >|  
|MyConfig|不适用|\<MyConfig Win64 设置 >|  
  
> [!NOTE]
> 无法创建不包含"Win32"平台，除非您的目标的项目不支持 Win32"MyConfig"解决方案配置。  
  
 更改活动解决方案配置该解决方案中选择一的生成、 运行、 调试或部署的项目配置。 例如，如果将活动解决方案配置从版本更改为调试，该解决方案中的所有项目中自动都生成解决方案的调试配置中所示的项目的配置。 项目的配置通常也是命名的调试除非用户已手动更改环境的配置管理器中。  
  
 存储为每个项目的解决方案配置属性包括项目名称、 项目配置名称、 标志以指示可以生成或部署，和平台名称。 有关详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。  
  
 用户可以查看和层次结构 （解决方案资源管理器） 中选择解决方案并打开属性页设置解决方案配置参数。 同样，可以查看和设置通过在解决方案资源管理器中选择一个项目并打开该项目的属性页的项目配置参数。  
  
 用户还可以生成一个项目使用发布配置设置和其他如有必要调试配置设置。 有关详细信息，请参阅[构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)。  
  
 下图显示了如何实现这些接口支持解决方案和项目配置：  
  
 ![配置界面图](../../extensibility/internals/media/vsconfiginterfaces.gif "vsConfigInterfaces")  
配置接口  
  
 与上面的关系图相关的一些注释：  
  
- `IDispatch` 标记为可选的配置对象中。 具体而言，是可选的能够浏览对象上的配置接口。  
  
- `IVsDebuggableProjectCfg` 标记为可选中配置对象，但需要调试支持。  
  
- `IVsProjectCfg2` 标记为可选中配置对象，但所需的输出分组的支持。  
  
- `Config Provider`对象标记为可选的对象，但是实现它的位置的选项。 项目对象或上一个单独的对象，可以实现对象。  
  
- `IVsCfgProvider2` 是所需的平台支持和配置编辑。 `IVsCfgProvider` 已足够，如果您不会实现该功能。  
  
- 在关系图中显示为单独的对象可以合并到同一个类，在实际应用中这些对象中的部分根据特定的设计要求。 在本部分的其他主题中，但是，对象和与这些对象关联的接口将讨论根据关系图中给出的方案。  
  
- 单独实现某些对象。 例如，项目和解决方案构建发生在单独的线程和要单独从对象，该对象描述生成的配置管理生成的生活的对象。  
  
  有关对配置对象接口和上图中的配置提供程序对象接口的详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)。 此外，[构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)在配置生成器并生成依赖项对象的接口，提供了详细信息和[用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)进一步描述附加到的配置部署人员和部署依赖关系对象的接口。 最后，[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)描述了输出组并输出对象的接口，以及如何使用属性页可以查看和设置配置相关的属性。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>   
 [用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)   
 [解决方案配置](../../extensibility/internals/solution-configuration.md)
