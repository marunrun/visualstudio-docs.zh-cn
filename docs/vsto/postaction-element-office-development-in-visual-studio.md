---
title: '&lt;&gt;Visual Studio 中的 postAction 元素 (Office 开发) '
ms.date: 02/02/2017
ms.topic: reference
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
ms.openlocfilehash: 149aa0cf8543f5b5b1b5ada18a8b2f0e58f063d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546934"
---
# <a name="ltpostactiongt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中的 postAction 元素 (Office 开发) 
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

### <a name="entrypoint"></a>entryPoint
 可选。 `entryPoint`命名空间中元素的角色 `vstav3` 是在[Visual Studio&#41;中 &#40;Office 开发&#60;s&#62; 元素](../vsto/entrypoints-element-office-development-in-visual-studio.md)中定义的。

### <a name="postactiondata"></a>postActionData
 可选。 `postActionData`命名空间中元素的角色 `vstav3` 是在[Visual Studio&#41;中 &#40;Office 开发&#60;postActionData&#62; 元素](../vsto/postactiondata-element-office-development-in-visual-studio.md)中定义的。

## <a name="post-deployment-action-example"></a>部署后操作示例

### <a name="description"></a>说明
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `postAction` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是 [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

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
