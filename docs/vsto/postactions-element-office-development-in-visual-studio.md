---
title: '&lt;&gt;Visual Studio 中的 postActions 元素 (Office 开发) '
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postActions> element
- postActions element
- <postActions> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bfe9ae171f0f6fac1c2b5add5340de1c11f3da0f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544412"
---
# <a name="ltpostactionsgt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中的 postActions 元素 (Office 开发) 
  `postActions` 命名空间的 `vstav3` 元素包含描述部署后操作（在安装 Office 解决方案后运行）的 `postAction` 所有元素。

## <a name="syntax"></a>语法

```xml
<postActions>
  <postAction>
    <entryPoint>
    </entryPoint>
    <postActionData>
    </postActionData>
  </postAction>
</postActions>
```

## <a name="elements-and-attributes"></a>元素和属性
 `postActions` 元素是可选的，它位于 `vstav3` 命名空间中。 在应用程序清单中定义的 `postActions` 元素只有一个。

 `postActions` 元素没有属性。

 `postActions` 具有以下元素。

### <a name="postaction"></a>postAction
 可选。 `postAction`命名空间中元素的角色 `vstav3` 是在[Visual Studio&#41;中 &#40;Office 开发&#60;postAction&#62; 元素](../vsto/postaction-element-office-development-in-visual-studio.md)中定义的。

## <a name="post-deployment-action-example"></a>部署后操作示例

### <a name="description"></a>说明
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `postActions` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是 [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstav3:postActions>
  <vstav3:postAction>
    <vstav3:entryPoint
      class="PostDeploymentAction.PostDeploymentActionSample">
      <assemblyIdentity
        name="PostDeploymentAction"
        version="1.0.0.0"
        language="neutral"
        processorArchitecture="msil" />
    </vstav3:entryPoint>
    <vstav3:postActionData>
    </vstav3:postActionData>
  </vstav3:postAction>
</vstav3:postActions>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
