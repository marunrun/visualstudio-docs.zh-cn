---
title: 配置选项概述 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709414"
---
# <a name="configuration-options-overview"></a>配置选项概述
中的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目可以支持可生成、调试、运行和/或部署的多个配置。 配置是使用一组命名属性（通常是编译器开关和文件位置）描述的生成类型。 默认情况下，新解决方案包含两个配置：*调试*和*发布*。 这些配置可以使用其默认设置应用，也可以修改以满足您的特定解决方案和/或项目要求。 某些包可以通过两种方式构建：作为 ActiveX 编辑器或作为就地组件。 但是，项目不需要支持多个配置。 如果只有一个配置可用，则该配置将映射到所有解决方案配置中。

 配置通常由两部分组成：配置名称（如*调试*或*发布*）和平台设置。 配置的平台名称标识配置目标的环境，如 API 集或操作系统平台。 用户不能[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]创建平台;他们必须从项目 VSPackage 允许的选择中进行选择。 当用户安装 VSPackage 时，在程序包开发期间创建的交付平台可以基于包创建者设置的任何条件显示所需的任何平台名称。 然后，用户可以在实例化属性页时，从通过 VSPackage 提供的平台列表中选择。

 平台名称是可选的，因为并非所有项目都支持平台的概念。 当配置缺少平台名称时，字符串**N/A**将显示在 UI 中。

 每个解决方案都有自己的配置集，其中只有一个一个可以一次处于活动状态。 解决方案配置是每个项目中不超过一个配置的一组。 "不超过"规定是由于可以选择将项目从解决方案配置中排除。 用户可以创建自己的自定义解决方案配置。

 下表说明了项目的典型配置设置。 行用配置名称和带有平台名称的列标记。

|配置名称|平台： Win32|平台： Win64|
|------------------------|----------------------|----------------------|
|*调试*|\<调试 win32 设置>|\<调试 Win64 设置>|
|*释放*|\<发布 Win32 设置>|\<发布 Win64 设置>|
|*我的康菲克*|空值|\<MyConfig Win64 设置>|

> [!NOTE]
> 除非您定位的项目不支持 Win32，否则您无法创建排除 Win32 平台的*MyConfig*解决方案配置。

 更改解决方案的活动配置将选择在该解决方案中生成、运行、调试或部署的项目配置集。 例如，如果将活动解决方案配置从 *"发布"* 更改为 *"调试*"，则该解决方案中的所有项目都将自动使用解决方案的调试配置中指示的项目配置生成。 除非用户已在环境的配置管理器中进行了手动更改，否则项目的配置也命名为*调试*。

 为每个项目存储的解决方案配置属性包括项目名称、项目配置名称、指示是生成还是部署的标志以及平台名称。 有关详细信息，请参阅[解决方案配置](../../extensibility/internals/solution-configuration.md)。

 用户可以通过在层次结构（解决方案资源管理器）中选择解决方案并打开属性页来查看和设置解决方案配置参数。 同样，您可以通过在解决方案资源管理器中选择项目并打开该项目的属性页来查看和设置项目配置参数。

 如有必要，用户还可以使用发布配置设置构建一个项目，其余项目使用调试配置设置。 有关详细信息，请参阅[用于构建 的项目配置](../../extensibility/internals/project-configuration-for-building.md)。

 下图显示了如何实现支持解决方案和项目配置的接口：

 ![配置接口图形](../../extensibility/internals/media/vsconfiginterfaces.gif "vs 配置接口")配置接口

 与上图有关的几条注释：

- `IDispatch`在配置对象中标记为可选。 具体而言，在浏览对象上具有配置接口是可选的。

- `IVsDebuggableProjectCfg`在配置对象中标记为可选，但调试支持是必需的。

- `IVsProjectCfg2`在配置对象中标记为可选，但需要输出分组支持。

- Config 提供程序对象被标记为可选对象，但选项是实现它的位置。 您可以在项目对象或单独对象上实现该对象。

- `IVsCfgProvider2`平台支持和配置编辑需要。 `IVsCfgProvider`如果不实现该功能，就足够了。

- 关系图中显示的一些对象作为单独的对象可以合并到同一类中，其中根据您的特定设计要求具有实用性。 但是，在本节中的其他主题中，将根据关系图中提供的方案讨论与这些对象关联的对象和接口。

- 某些对象是单独实现的。 例如，项目和解决方案构建发生在单独的线程上，用于管理生成生活的对象与描述生成配置的对象分开。

  有关上一图中的配置对象接口和配置提供程序对象接口的详细信息，请参阅 Project[配置对象](../../extensibility/internals/project-configuration-object.md)。 此外，[用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)提供了有关配置生成器和生成依赖项对象接口的详细信息，[用于管理部署的项目配置](../../extensibility/internals/project-configuration-for-managing-deployment.md)进一步描述了附加到配置部署者和部署依赖项对象的接口。 最后，[输出的项目配置](../../extensibility/internals/project-configuration-for-output.md)描述了输出组和输出对象接口，以及使用属性页来查看和设置与配置相关的属性。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>
- [用于构建的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
