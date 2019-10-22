---
title: '&lt;loc&gt; (JavaScript) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <loc> JavaScript XML tag
- loc JavaScript XML tag
ms.assetid: 0d3349b6-4bdd-418f-bc11-73665305baae
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cf6016b2c12fd5ebe7cfb76c14c776508d99d2db
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651481"
---
# <a name="ltlocgt-javascript"></a>&lt;loc&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定提供本地化 IntelliSense 信息的挎斗文件的位置和类型。

## <a name="syntax"></a>语法

```
<loc filename="filename"
    format="vsdoc|messagebundle" />
```

#### <a name="parameters"></a>参数
 `filename`（可选）。 挎斗文件的根名称，该文件包含非特定区域性的本地化信息。 当 Visual Studio 搜索本地化信息时，它会尝试查找此文件的特定于区域性的版本。 例如，如果 `filename` 为 jquery .xml，Visual Studio 会在与包含 `<loc>` 元素的 .js 文件相同的位置中搜索正确的区域性特定文件夹（如 JA）。 如果它找到特定于区域性的文件夹，它将检查 jquery .xml 文件是否存在于该文件夹中。 如果它找不到正确的文件，则使用托管资源位置规则。 @No__t_0 的默认值是当前文件的名称，但使用 .xml 扩展名而不是 .js。

 `format`（可选）。 用于本地化的挎斗文件的类型。 使用 `messagebundle` 指定由开放式 Ajax 元数据定义的消息绑定的使用。 建议使用 `messagebundle` 格式。 但是，在 Microsoft Ajax 或 winmd 文件中不支持此格式。 使用 `vsdoc` 指定 Microsoft Ajax 和 Windows 运行时所使用的标准 .NET Framework 本地化格式。 此属性是可选的。 `vsdoc` 是默认格式。

## <a name="remarks"></a>备注
 @No__t_0 元素必须出现在与 `<reference>` 元素相同的节中的文件顶部。 @No__t_0 元素的使用规则与 `<reference>` 元素相同。 有关详细信息，请参阅[JavaScript IntelliSense](../ide/javascript-intellisense.md)中的 "引用指令" 一节。

 Visual Studio 处理每个 .js 文件的单个 `<loc>` 元素。 如果存在多个 `<loc>` 元素，则只使用单个 `<loc>` 元素。 确定要使用的 `<loc>` 元素的行为未定义。

 使用消息包格式时，请使用 XML 文档注释中的 `locid` 特性来指定 `name` 特性值。

## <a name="example"></a>示例
 下面的示例演示如何使用 messagebundle 格式的 `<loc>` 元素。 将以下 XML 添加到名为 messageFilename 的文件，并将该文件放入正确的区域性特定的文件夹中，如 `filename` 参数的描述中所指定。

```
<?xml version="1.0" encoding="utf-8" ?>
<messagebundle>
  <msg name="1">A class that represents a rectangle</msg>
  <msg name="2">The height of a rectangle</msg>
  <msg name="3">The width of a rectangle</msg>
</messagebundle>

```

 对于 messagebundle 示例，请将以下代码添加到项目中的 JavaScript 文件。 @No__t_0 元素必须出现为 JavaScript 文件中的第一行。 此代码中的说明将替换为本地化说明（如果可用）。

```javascript
/// <loc filename="messageFilename.xml" format="messagebundle"/>

function doSomething(a,b)
{
    /// <summary locid='1'>description</summary>
    /// <param name='a' locid='2'>parameter a description</param>
    /// <param name='b' locid='3'>parameter b description</param>
}

```

 下面的示例使用 VSDoc 格式。 将以下 XML 添加到名为 scriptFilename 的文件，并将该文件放在正确的特定于区域性的文件夹中。

```
<?xml version="1.0" encoding="utf-8" ?>
<doc>
  <assembly>
    <name>Lights</name>
  </assembly>
  <members>
    <member name="M:illuminate">
      <summary>Activates a light. </summary>
      <param name='a'>The light to activate. </param>
    </member>
  </members>
</doc>

```

 对于 VSDoc 示例，请将以下代码添加到项目中的 JavaScript 文件。 此代码中的说明将替换为本地化说明（如果可用）。

```javascript
/// <loc filename="scriptFilename.xml" format="vsdoc" />

function illuminate(a)
{
    /// <summary locid='M:illuminate'>description</summary>
    /// <param name='a' type='Number'>parameter a description</param>
}

```

## <a name="see-also"></a>另请参阅
 [XML 文档注释](../ide/xml-documentation-comments-javascript.md)
