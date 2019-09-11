---
title: '&lt;deployment&gt;元素（ClickOnce 部署） |Microsoft Docs'
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
ms.openlocfilehash: 988ce0859ab24377395cc4077f9e6fa42e0487a5
ms.sourcegitcommit: 4dfe098ac0df294aad63e6b384d6575980798ca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70887853"
---
# <a name="ltdeploymentgt-element-clickonce-deployment"></a>&lt;deployment&gt;元素（ClickOnce 部署）
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
 `deployment` 元素是必需的，它位于 `urn:schemas-microsoft-com:asm.v2` 命名空间中。 元素具有以下属性。

| 特性 | 描述 |
|--------------------------| - |
| `install` | 必需。 指定此应用程序是否在 Windows "**开始**" 菜单和 "控制面板" 的 "**添加或删除程序**" 应用程序中定义状态。 有效值为 `true` 和 `false`。 如果`false`为[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，将始终从网络中运行此应用程序的最新版本， `subscription`并且将无法识别元素。 |
| `minimumRequiredVersion` | 可选。 指定可在客户端上运行的此应用程序的最低版本。 如果应用程序的版本号小于部署清单中提供的版本号，则应用程序将不会运行。 版本号必须以格式`N.N.N.N`指定，其中`N`是无符号整数。 如果特性为`false` ，`minimumRequiredVersion`则不得设置。 `install` |
| `mapFileExtensions` | 可选。 默认为 `false`。 如果`true`为，则部署中的所有文件都必须具有 .deploy 扩展名。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]从 Web 服务器下载这些文件后，会立即将其从 Web 服务器中去除。 如果使用[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]发布应用程序，它会自动将此扩展添加到所有文件。 此参数允许从 Web 服务器下载[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署中的所有文件，这些文件阻止以 "不安全" 扩展（如 .exe）结尾的文件的传输。 |
| `disallowUrlActivation` | 可选。 默认为 `false`。 如果`true`为，则通过单击 url 或在 Internet Explorer 中输入 url 来阻止已安装的应用程序启动。 如果该`install`属性不存在，则忽略此属性。 |
| `trustURLParameters` | 可选。 默认为 `false`。 如果`true`为，则允许 URL 包含传入应用程序的查询字符串参数，非常类似于将命令行自变量传递到命令行应用程序。 有关详细信息，请参阅[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)。<br /><br /> 如果特性为`true` `false`， `trustUrlParameters`则必须从清单中排除，或者显式设置为。 `disallowUrlActivation` |

 `deployment`元素还包含下列子元素。

## <a name="subscription"></a>订阅
 可选。 `update`包含元素。 `subscription` 元素没有属性。 如果该`subscription`元素不存在，则[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序将从不扫描更新。 `deployment` `false` `subscription`如果元素的`install`属性为[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，则将忽略元素，因为从网络启动的应用程序始终使用最新版本。

## <a name="update"></a>更新
 必需。 此元素是`subscription`元素的子元素，并且包含`beforeApplicationStartup`或`expiration`元素。 `beforeApplicationStartup`不`expiration`能在同一部署清单中同时指定和。

 `update` 元素没有属性。

## <a name="beforeapplicationstartup"></a>beforeApplicationStartup
 可选。 此元素是`update`元素的子元素，但没有属性。 如果该`beforeApplicationStartup`元素存在，则在检查更新时[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，如果客户端处于联机状态，则应用程序将被阻止。 如果此元素不存在， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]将首先根据为`expiration`元素指定的值扫描更新。 `beforeApplicationStartup`不`expiration`能在同一部署清单中同时指定和。

## <a name="expiration"></a>过期
 可选。 此元素是`update`元素的子元素，没有任何子级。 `beforeApplicationStartup`不`expiration`能在同一部署清单中同时指定和。 当发生更新检查并检测到更新版本时，新版本将在现有版本运行时缓存。 然后，新版本将在下一次启动[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序时安装。

 `expiration`元素支持以下特性。

|特性|描述|
|---------------|-----------------|
|`maximumAge`|必需。 标识当前更新在应用程序执行更新检查之前应如何发生。 时间单位由`unit`属性确定。|
|`unit`|必需。 标识的时间`maximumAge`单位。 有效单位为`hours`、 `days`和`weeks`。|

## <a name="deploymentprovider"></a>deploymentProvider
 对于 .NET Framework 2.0，如果部署清单包含`subscription`部分，则此元素是必需的。 对于 .NET Framework 3.5 及更高版本，此元素是可选的，它将默认为发现部署清单的服务器和文件路径。

 此元素是 `deployment` 元素的子元素，并且包含以下元素。

| 特性 | 描述 |
|------------| - |
| `codebase` | 必需。 标识用于更新[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序的部署清单的位置，作为一个统一资源标识符（URI）。 此元素还允许将更新位置转发到基于 CD 的安装。 必须是有效的 URI。 |

## <a name="remarks"></a>备注
 你可以将[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序配置为在启动时扫描更新、在启动后扫描更新或从不检查更新。 若要在启动时扫描更新，请确保`beforeApplicationStartup`元素`update`下存在元素。 若要在启动后扫描更新，请确保`expiration`元素`update`下存在元素，并提供更新间隔。

 若要禁用检查更新，请删除`subscription`元素。 当你在部署清单中指定从不扫描更新时，你仍可以使用<xref:System.Deployment.Application.ApplicationDeployment.CheckForUpdate%2A>方法手动检查更新。

 有关 deploymentProvider 如何与更新相关的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

## <a name="examples"></a>示例
 下面的代码示例阐释了`deployment` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署清单中的元素。 该示例使用`deploymentProvider`元素来指示首选的更新位置。

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