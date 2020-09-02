---
title: 配置选项概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations
- configuration options, about configuration options
ms.assetid: f4ad4dd3-b39e-42df-ad89-d403cdf24a2b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6d5ac25fcef7b942b791402baf17982c9810e92a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709414"
---
# <a name="configuration-options-overview"></a>配置选项概述
中的项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可以支持可生成、调试、运行和/或部署的多个配置。 配置是用命名的属性集（通常是编译器开关和文件位置）描述的生成类型。 默认情况下，新的解决方案包含两个配置： " *调试* " 和 " *发布*"。 可以使用默认设置应用这些配置，或修改这些配置以满足特定的解决方案和/或项目要求。 可以通过两种方式生成某些包：作为 ActiveX 编辑器或就地组件。 但项目不需要支持多个配置。 如果只有一个配置可用，则该配置将映射到所有解决方案配置中。

 配置通常由两部分组成：配置名称 (如 " *调试* " 或 " *发布* ") 和平台设置。 配置的平台名称标识配置的目标环境，如 API 集或操作系统平台。 的用户 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 无法创建平台; 他们必须从项目 VSPackage 允许的选项中进行选择。 当用户安装 VSPackage 时，在包开发过程中创建的交付平台可以根据包创建者所设置的任何标准来呈现任何所需的平台名称。 然后，用户可以在属性页实例化时通过 VSPackage 提供的平台列表中进行选择。

 平台名称是可选的，因为并非所有项目都支持平台的概念。 当配置缺少平台名称时，UI 中会显示字符串 **N/a** 。

 每个解决方案都有其自己的一组配置，一次只能有一个处于活动状态。 解决方案配置是每个项目中的一组不是多个配置。 "不超过" stipulation 的原因是从解决方案配置中排除项目的选项。 用户可以创建自己的自定义解决方案配置。

 下表说明了项目的典型配置。 行标有配置名称和平台名称的列。

|配置名称|平台： Win32|平台： Win64|
|------------------------|----------------------|----------------------|
|*调试*|\<Debug Win32 settings>|\<Debug Win64 settings>|
|*版本*|\<Release Win32 settings>|\<Release Win64 settings>|
|*Myconfig.xml*|空值|\<MyConfig Win64 settings>|

> [!NOTE]
> 不能创建排除 Win32 平台的 *myconfig.xml* 解决方案配置，除非目标项目不支持 win32。

 更改解决方案的活动配置可选择在该解决方案中生成、运行、调试或部署的项目配置集。 例如，如果您将活动解决方案配置从 " *发布* " 更改为 " *调试*"，则该解决方案中的所有项目都将自动用解决方案的 "调试" 配置中指示的项目配置生成。 项目的配置也称为 *调试* ，除非用户在环境的 Configuration Manager 中进行了手动更改。

 为每个项目存储的解决方案配置属性包括项目名称、项目配置名称、标志，用于指示是生成还是部署，以及平台名称。 有关详细信息，请参阅 [解决方案配置](../../extensibility/internals/solution-configuration.md)。

 用户可以通过选择层次结构中的解决方案来查看和设置解决方案配置参数， (解决方案资源管理器) 并打开属性页。 同样，您可以通过在解决方案资源管理器中选择一个项目，然后打开该项目的属性页来查看和设置项目配置参数。

 用户还可以使用 "发布" 配置设置生成一个项目，并在必要时使用 "调试" 配置设置。 有关详细信息，请参阅 [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)。

 下图显示了如何实现支持解决方案和项目配置的接口：

 ![配置界面图](../../extensibility/internals/media/vsconfiginterfaces.gif "vsConfigInterfaces") 配置接口

 与上一关系图相关的一些说明：

- `IDispatch` 在配置对象中标记为可选。 具体而言，可以选择在浏览对象上设置配置接口。

- `IVsDebuggableProjectCfg` 在配置对象中标记为可选，但对于调试支持是必需的。

- `IVsProjectCfg2` 在配置对象中标记为可选，但对于输出分组支持是必需的。

- Config 提供程序对象被标记为可选对象，但选项是实现它的位置。 您可以在项目对象或单独的对象上实现对象。

- `IVsCfgProvider2` 平台支持和配置编辑需要。 `IVsCfgProvider` 如果不实现该功能，就足够了。

- 此关系图中显示为单独对象的某些对象可以组合到同一个类中，具体取决于特定的设计要求。 但在本节的其他主题中，将根据关系图中显示的方案讨论与这些对象关联的对象和接口。

- 某些对象是单独实现的。 例如，在单独的线程上生成项目和解决方案，并将该对象与描述生成配置的对象分开管理。

  有关上图中的配置对象接口和配置提供程序对象接口的详细信息，请参阅 [项目配置对象](../../extensibility/internals/project-configuration-object.md)。 此外， [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md) 提供了有关配置生成器和构建依赖对象接口的详细信息，以及 [用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md) 。 最后， [输出的项目配置](../../extensibility/internals/project-configuration-for-output.md) 描述输出组和输出对象接口，并使用属性页查看和设置依赖于配置的属性。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
