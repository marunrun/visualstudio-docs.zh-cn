---
title: '&lt;postAction&gt;元素 （Visual Studio 中的 Office 开发）'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postAction> element
- <postAction> element
- postAction element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 53cf47ef9a78ebb54c377e19b4f7fbad444bbfcd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976531"
---
# <a name="ltpostactiongt-element-office-development-in-visual-studio"></a>&lt;postAction&gt;元素 （Visual Studio 中的 Office 开发）
  `postAction` 命名空间的 `vstav3` 元素包含与部署后操作（在安装 Office 解决方案后运行）相关联的 `entrypoint` 元素和所有 `postActionData` 元素。

## <a name="syntax"></a>语法

```xml
<postAction>
  <entryPoint>
  </entryPoint>
  <postActionData>
  </postActionData>
</postAction>
```

## <a name="elements-and-attributes"></a>元素和属性
 `postAction` 元素是可选的，它位于 `vstav3` 命名空间中。 每个部署后操作的应用程序清单中只定义了一个 `postAction` 元素。

 `postAction` 元素没有属性。

 `postAction` 具有下列元素。

### <a name="entrypoint"></a>entrypoint
 可选。 角色`entryPoint`中的元素`vstav3`中定义命名空间[&#60;的入口点&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)。

### <a name="postactiondata"></a>postActionData
 可选。 角色`postActionData`中的元素`vstav3`中定义命名空间[ &#60;postActionData&#62;元素&#40;Visual Studio 中的 Office 开发&#41;](../vsto/postactiondata-element-office-development-in-visual-studio.md)。

## <a name="post-deployment-action-example"></a>部署后操作示例

### <a name="description"></a>描述
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `postAction` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例摘自[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
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
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
