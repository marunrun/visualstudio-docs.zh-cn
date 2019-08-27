---
title: 将名称参数添加到项目和项模板
ms.date: 01/02/2018
ms.topic: conceptual
helpviewer_keywords:
- template parameters
- template parameters, substituting
- Visual Studio templates, using parameters
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cf9a990be3f5e87180967a4f9f274ec79fbc357e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62946872"
---
# <a name="how-to-substitute-parameters-in-a-template"></a>如何：替换模板中的参数

使用模板参数，可在从模板创建文件时替换标识符，例如类名称和命名空间。 可将模板参数添加到现有模板，或使用模板参数创建模板。

模板参数是以 $参数$ 格式编写的。 有关模板参数的完整列表，请参阅[模板参数](../ide/template-parameters.md)。

以下部分演示了如何修改模板，以将命名空间的名称替换为“安全项目名称”。

## <a name="example---namespace-name"></a>示例 - 命名空间名称

1. 将参数插入模板中的一个或多个代码文件中。 例如:

    ```csharp
    namespace $safeprojectname$
    ```

1. 在模板的 vstemplate  文件中，找到包括此文件的 `ProjectItem` 元素。

1. 将 `ProjectItem` 元素的 `ReplaceParameters` 属性设置为 `true`：

    ```xml
    <ProjectItem ReplaceParameters="true">Class1.cs</ProjectItem>
    ```

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [模板参数](../ide/template-parameters.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [ProjectItem 元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)