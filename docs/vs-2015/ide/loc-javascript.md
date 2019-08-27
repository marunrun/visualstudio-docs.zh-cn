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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8029dc6282e7b5a4ff9075257bcb1b6213a4a6b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186105"
---
# <a name="ltlocgt-javascript"></a>&lt;loc&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定的位置和提供智能感知的本地化的信息的挎斗文件的类型。  
  
## <a name="syntax"></a>语法  
  
```  
<loc filename="filename"  
    format="vsdoc|messagebundle" />  
```  
  
#### <a name="parameters"></a>参数  
 `filename`  
 可选。 包含非特定区域性的本地化信息的挎斗文件的根名称。 当 Visual Studio 将本地化信息时，它会尝试查找此文件的特定于区域性的版本。 例如，如果`filename`是 jquery.xml，正确特定于区域性的文件夹 （如 JA) 中包含的.js 文件与相同的位置的 Visual Studio 搜索`<loc>`元素。 如果它找到的特定于区域性的文件夹，它会检查其中是否存在 jquery.xml 文件。 如果找不到正确的文件，则改为使用托管的资源位置规则。 默认值为`filename`是当前的文件，而不是.js 扩展名为.xml 的名称。  
  
 `format`  
 可选。 用于本地化的挎斗文件的类型。 使用`messagebundle`若要指定打开 Ajax 元数据定义的消息绑定的使用。 `messagebundle` 是建议的格式。 但是，在 Microsoft Ajax 或.winmd 文件中不支持此格式。 使用`vsdoc`指定 Microsoft Ajax 和 Windows 运行时使用的标准.NET Framework 本地化格式。 此属性是可选的。 `vsdoc` 是默认格式。  
  
## <a name="remarks"></a>备注  
 `<loc>`元素必须出现在相同的部分中的文件的顶部`<reference>`元素。 为规则使用情况`<loc>`元素将与相同`<reference>`元素。 有关详细信息，请参阅中的"引用指令"一节[JavaScript IntelliSense](../ide/javascript-intellisense.md)。  
  
 Visual Studio 处理单个`<loc>`每个.js 文件的元素。 如果多个`<loc>`元素不存在，只有一个`<loc>`使用元素。 用于确定哪些行为`<loc>`未定义要使用的元素。  
  
 使用消息捆绑包格式时，使用`locid`属性中指定的 XML 文档注释`name`属性值。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`<loc>`messagebundle 格式的元素。 将以下 XML 添加到名为 messageFilename.xml 的文件并将文件放在正确的特定于区域性的文件夹中的说明指定`filename`参数。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<messagebundle>  
  <msg name="1">A class that represents a rectangle</msg>  
  <msg name="2">The height of a rectangle</msg>  
  <msg name="3">The width of a rectangle</msg>  
</messagebundle>  
  
```  
  
 Messagebundle 示例中，将以下代码添加到项目中的 JavaScript 文件。 `<loc>`元素必须出现在 JavaScript 文件中的第一行。 如果可用，将会在此代码中的说明被本地化说明。  
  
```javascript  
/// <loc filename="messageFilename.xml" format="messagebundle"/>  
  
function doSomething(a,b)   
{  
    /// <summary locid='1'>description</summary>  
    /// <param name='a' locid='2'>parameter a description</param>  
    /// <param name='b' locid='3'>parameter b description</param>  
}  
  
```  
  
 下面的示例使用 VSDoc 格式。 将以下 XML 添加到名为 scriptFilename.xml 的文件并将文件放在正确的特定于区域性的文件夹。  
  
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
  
 VSDoc 示例中，将以下代码添加到项目中的 JavaScript 文件。 如果可用，将会在此代码中的说明被本地化说明。  
  
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
