---
title: '&lt;部署&gt;元素 （ClickOnce 部署） |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#subscription
- urn:schemas-microsoft-com:asm.v2#beforeApplicationStartup
- urn:schemas-microsoft-com:asm.v2#deploymentProvider
- urn:schemas-microsoft-com:asm.v2#update
- urn:schemas-microsoft-com:asm.v2#deployment
- urn:schemas-microsoft-com:asm.v2#expiration
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <deployment> element [ClickOnce deployment manifest]
ms.assetid: 4fafa9c2-97a0-4cea-b8fd-9746dca33af4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 90168dd760ba5619e2d50c864f54122b01ed66fa
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928934"
---
# <a name="ltdeploymentgt-element-clickonce-deployment"></a>&lt;部署&gt;元素 （ClickOnce 部署）
标识用于部署更新并向系统公开的特性。

## <a name="syntax"></a>语法

```xml

      <deployment
   install
   minimumRequiredVersion
   mapFileExtensions
   disallowUrlActivation
   trustUrlParameters
>
   <subscription>
         <update>
            <beforeApplicationStartup/>
            <expiration
               maximumAge
               unit
            />
         </update>
   </subscription>
   <deploymentProvider
      codebase
   />
</deployment>
```

## <a name="elements-and-attributes"></a>元素和属性
 `deployment` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v1` 命名空间中。 元素具有以下属性。

| 特性 | 描述 |
|--------------------------| - |
| `install` | 必需。 指定此应用程序是否在 Windows 上定义一个快捷**启动**菜单控件面板和**添加或删除程序**应用程序。 有效值为 `true` 和 `false`。 如果`false`，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]始终会从网络运行此应用程序的最新版本并将无法识别`subscription`元素。 |
| `minimumRequiredVersion` | 可选。 指定可在客户端运行此应用程序的最低版本。 如果应用程序的版本编号小于提供的部署清单中的版本号，不会运行该应用程序。 必须以格式指定版本号`N.N.N.N`，其中`N`是一个无符号的整数。 如果`install`属性是`false`，`minimumRequiredVersion`不能设置。 |
| `mapFileExtensions` | 可选。 默认为 `false`。 如果`true`，部署中的所有文件必须都具有.deploy 扩展名。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将关闭这些文件中剥离此扩展，只要它从 Web 服务器下载它们。 如果使用发布你的应用程序，则[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，它会自动将此扩展添加到的所有文件。 此参数允许内的所有文件[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署，以从筛选器阻止传输的"不安全"扩展，如.exe 结尾的文件的 Web 服务器下载。 |
| `disallowUrlActivation` | 可选。 默认为 `false`。 如果`true`，可以防止通过单击的 URL 或 Internet 资源管理器中输入 URL 来启动已安装应用程序。 如果`install`属性不存在，则忽略此属性。 |
| `trustURLParameters` | 可选。 默认为 `false`。 如果`true`，可以包含查询字符串参数传递到应用程序的 URL，太多类似的命令行自变量传递给命令行应用程序。 有关详细信息，请参阅[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。<br /><br /> 如果`disallowUrlActivation`属性是`true`，`trustUrlParameters`必须是从在清单中排除或显式设置为`false`。 |

 `deployment`元素还包含以下子元素。

## <a name="subscription"></a>订阅
 可选。 包含`update`元素。 `subscription` 元素没有属性。 如果`subscription`元素不存在，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序将永远不会扫描更新。 如果`install`的属性`deployment`元素是`false`，则`subscription`忽略元素，因为[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]启动应用程序是从网络始终使用最新版本。

## <a name="update"></a>更新
 必需。 此元素是子元素的`subscription`元素，它包含`beforeApplicationStartup`或`expiration`元素。 `beforeApplicationStartup` 和`expiration`无法同时指定相同的部署清单中。

 `update` 元素没有属性。

## <a name="beforeapplicationstartup"></a>beforeApplicationStartup
 可选。 此元素是子元素的`update`元素并且没有任何特性。 当`beforeApplicationStartup`元素存在，该应用程序将被阻止时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]检查更新，如果客户端处于联机状态。 此元素不存在，如果[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]基于指定的值的更新将首先扫描`expiration`元素。 `beforeApplicationStartup` 和`expiration`无法同时指定相同的部署清单中。

## <a name="expiration"></a>过期
 可选。 此元素是子元素的`update`元素，并没有任何子级。 `beforeApplicationStartup` 和`expiration`无法同时指定相同的部署清单中。 当进行更新检查以及检测到更新的版本时，新版本缓存的现有版本运行时。 然后安装新版本的在下次启动[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序。

 `expiration`元素支持以下属性。

|特性|描述|
|---------------|-----------------|
|`maximumAge`|必需。 标识如何旧当前更新应会在之前在应用程序执行更新检查。 时间单位由`unit`属性。|
|`unit`|必需。 标识的时间单位`maximumAge`。 有效的单位为`hours`， `days`，和`weeks`。|

## <a name="deploymentprovider"></a>deploymentProvider
 为.NET Framework 2.0 中，如果此元素是必需部署清单包含`subscription`部分。 .NET Framework 3.5 及更高版本，此元素是可选的并将默认为服务器和在其中发现的部署清单的文件路径。

 此元素是 `deployment` 元素的子元素，并且包含以下元素。

| 特性 | 描述 |
|------------| - |
| `codebase` | 必需。 标识的位置，作为统一资源标识符 (URI)，用于更新部署清单的[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序。 此元素还允许转发的基于 CD 的安装的更新位置。 必须是有效的 URI。 |

## <a name="remarks"></a>备注
 你可以配置在[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]扫描在启动时，更新的应用程序在启动后检查更新或从不检查更新。 若要检查在启动更新，请确保`beforeApplicationStartup`元素下存在`update`元素。 若要在启动后检查更新，请确保`expiration`元素下存在`update`元素，并提供更新的时间间隔。

 若要禁用检查更新，请删除`subscription`元素。 当您指定永远不会扫描更新的部署清单中时，您可以仍手动检查更新使用<xref:System.Deployment.Application.ApplicationDeployment.CheckForUpdate%2A>方法。

 DeploymentProvider 如何与更新相关联的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

## <a name="examples"></a>示例
 下面的代码示例演示`deployment`中的元素[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署清单。 该示例使用`deploymentProvider`元素以指示首选的更新位置。

```xml
<deployment install="true" minimumRequiredVersion="2.0.0.0" mapFileExtension="true" trustUrlParameters="true">
    <subscription>
      <update>
        <expiration maximumAge="6" unit="hours" />
      </update>
    </subscription>
    <deploymentProvider codebase="http://www.adatum.com/MyApplication.application" />
  </deployment>
```

## <a name="see-also"></a>请参阅
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)