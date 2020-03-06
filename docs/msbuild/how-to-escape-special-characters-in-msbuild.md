---
title: 如何：转义 MSBuild 中的特殊字符 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- special characters, escaping
- characters, escapes
- escape characters
- MSBuild, escaping special characters
ms.assetid: 1aa3669c-1647-4960-b770-752e2532102f
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f9958ae93e2605ad3c89decb4ac9fabc18102148
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633871"
---
# <a name="how-to-escape-special-characters-in-msbuild"></a>如何：转义 MSBuild 中的特殊字符

某些字符在 MSBuild 项目文件中具有特殊意义。 例如，这些字符包括分号 (`;`) 和星号 (`*`)。 有关这些特殊字符的完整列表，请参阅 [MSBuild 特殊字符](../msbuild/msbuild-special-characters.md)。

若要将这些特殊字符用作项目文件中的文本，必须使用语法 `%<xx>` 指定它们，其中 `<xx>` 表示字符的 ASCII 十六进制值。

## <a name="msbuild-special-characters"></a>MSBuild 特殊字符

一个使用特殊字符的例子便是项列表的 `Include` 属性。 例如，以下项列表声明两个项：MyFile.cs 和 MyClass.cs   。

```xml
<Compile Include="MyFile.cs;MyClass.cs"/>
```

若要声明名称中包含分号的项，必须使用 `%<xx>` 语法转义分号，并阻止 MSBuild 声明两个独立项。 例如，以下项转义分号，并且声明一个名为 `MyFile.cs;MyClass.cs` 的项。

```xml
<Compile Include="MyFile.cs%3BMyClass.cs"/>
```

也可以使用[属性函数](../msbuild/property-functions.md)转义字符串。 例如，下面的示例等效于上面的示例。

```xml
<Compile Include="$([MSBuild]::Escape('MyFile.cs;MyClass.cs'))" />
```

### <a name="to-use-an-msbuild-special-character-as-a-literal-character"></a>将 MSBuild 特殊字符用作文本字符

使用表示法 `%<xx>` 替换特殊字符，其中 `<xx>` 表示 ASCII 字符的十六进制值。 例如，若要将星号 (`*`) 用作文本字符，请使用值 `%2A`。

## <a name="see-also"></a>请参阅
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [MSBuild](../msbuild/msbuild.md)
- [项](../msbuild/msbuild-items.md)
