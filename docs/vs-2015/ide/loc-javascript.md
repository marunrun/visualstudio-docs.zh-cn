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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
 `filename`（可选）。 挎斗文件的根名称，该文件包含非特定区域性的本地化信息。 当 Visual Studio 搜索本地化信息时，它会尝试查找此文件的特定于区域性的版本。 例如，如果 `filename` 是 jquery.xml，则 Visual Studio 会在与包含元素的 .js 文件相同的位置中搜索与 JA) 相同的正确区域性特定文件夹 (。 `<loc>` 如果它找到特定于区域性的文件夹，则会检查其中是否存在 jquery.xml 文件。 如果它找不到正确的文件，则使用托管资源位置规则。 的默认值 `filename` 是当前文件的名称，但使用 .xml 扩展名而不是 .js。

 `format`（可选）。 用于本地化的挎斗文件的类型。 用于 `messagebundle` 指定使用由开放式 Ajax 元数据定义的消息绑定的用法。 `messagebundle` 建议采用的格式。 但是，在 Microsoft Ajax 或 winmd 文件中不支持此格式。 使用 `vsdoc` 指定 Microsoft Ajax 和 Windows 运行时使用的标准 .NET Framework 本地化格式。 此属性是可选的。 `vsdoc` 是默认格式。

## <a name="remarks"></a>备注
 `<loc>`元素必须出现在与元素相同的节中的文件的顶部 `<reference>` 。 元素的使用规则与 `<loc>` `<reference>` 元素相同。 有关详细信息，请参阅 [JavaScript IntelliSense](../ide/javascript-intellisense.md)中的 "引用指令" 一节。

 Visual Studio 处理 `<loc>` 每个 .js 文件的单个元素。 如果存在多个 `<loc>` 元素， `<loc>` 则只使用单个元素。 确定 `<loc>` 要使用的元素的行为未定义。

 使用消息包格式时，请使用 `locid` XML 文档注释中的属性指定 `name` 属性值。

## <a name="example"></a>示例
 下面的示例演示如何使用 `<loc>` messagebundle 格式的元素。 将以下 XML 添加到名为 messageFilename.xml 的文件中，并将该文件放在参数说明中指定的正确的区域性特定文件夹中 `filename` 。

```
<?xml version="1.0" encoding="utf-8" ?>
<messagebundle>
  <msg name="1">A class that represents a rectangle</msg>
  <msg name="2">The height of a rectangle</msg>
  <msg name="3">The width of a rectangle</msg>
</messagebundle>

```

 对于 messagebundle 示例，请将以下代码添加到项目中的 JavaScript 文件。 `<loc>`元素必须出现为 JavaScript 文件中的第一行。 此代码中的说明将替换为本地化说明（如果可用）。

```javascript
/// <loc filename="messageFilename.xml" format="messagebundle"/>

function doSomething(a,b)
{
    /// <summary locid='1'>description</summary>
    /// <param name='a' locid='2'>parameter a description</param>
    /// <param name='b' locid='3'>parameter b description</param>
}

```

 下面的示例使用 VSDoc 格式。 将以下 XML 添加到名为 scriptFilename.xml 的文件，并将该文件放在正确的特定于区域性的文件夹中。

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
