---
title: CA1704:标识符应正确拼写
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8dbfc8081f980b7b9e978da782f1627a88a716a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809403"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704:标识符应正确拼写

|||
|-|-|
|TypeName|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因

标识符名称包含一个或多个未被 Microsoft 拼写检查器库识别的单词。 此规则不会不检查构造函数或特殊名称的成员，如 get 和 set 属性访问器。

## <a name="rule-description"></a>规则说明

此规则将标识符分析为令牌，并检查每个标记的拼写。 分析算法会执行以下转换：

- 以大写字母开头的新令牌。 例如，MyNameIsJoe 基于"我的"、"Name"、"Is"、"Joe"进行标记。

- 对于多个大写字母，最后一个大写字母开始一个新的标记。 例如，GUIEditor 基于到"GUI"，"编辑器"进行标记。

- 删除前导空格和尾随撇号。 例如，发件人基于向"发件人"进行标记。

- 下划线表示标记的末尾，并删除。 例如，Hello_world 基于进行标记为"Hello"，"world"。

- 将删除嵌入的与号。 例如，对于 & mat 标记化为"format"。

## <a name="language"></a>语言

当前仅对基于英语的区域性字典检查，拼写检查器。 可以通过添加更改项目文件中的项目的区域性**CodeAnalysisCulture**元素。

例如：

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> 如果将区域性设置为基于英语的区域性之外的任何内容，则以无提示方式禁用此代码分析规则。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请更正该单词的拼写或将该词添加到自定义字典。

### <a name="to-add-words-to-a-custom-dictionary"></a>若要向自定义词典添加单词

自定义词典 XML 文件命名*CustomDictionary.xml*。 将项目目录中，工具的安装目录中或与用户的配置文件下工具相关联的目录中放置字典 (*%USERPROFILE%\Application 数据\\...*).若要了解如何将自定义词典添加到 Visual Studio 中的项目，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)。

- 添加不应导致违反了字典/单词/识别路径下的字词。

- 添加应导致违反了无法识别的单词/字典/路径下的字词。

- 添加单词应将标记为过时已弃用的单词/字典/路径下。 请参阅相关的规则主题[CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)有关详细信息。

- 将异常添加到字典/首字母缩写词/CasingExceptions 路径的首字母缩略词大小写规则。

以下是自定义字典文件结构的示例：

```xml
<Dictionary>
   <Words>
      <Unrecognized>
         <Word>cb</Word>
      </Unrecognized>
      <Recognized>
         <Word>stylesheet</Word>
         <Word>GotDotNet</Word>
      </Recognized>
      <Deprecated>
         <Term PreferredAlternate="EnterpriseServices">ComPlus</Term>
      </Deprecated>
   </Words>
   <Acronyms>
      <CasingExceptions>
         <Acronym>CJK</Acronym>
         <Acronym>Pi</Acronym>
      </CasingExceptions>
   </Acronyms>
</Dictionary>
```

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

仅当是故意拼错单词和单词适用于一组有限的库，禁止显示此规则的警告。 正确的拼写的单词可以减少所需的新软件库的学习曲线。

## <a name="related-rules"></a>相关的规则

- [CA2204:应正确拼写文本](../code-quality/ca2204-literals-should-be-spelled-correctly.md)
- [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708:标识符不应不同于用例的详细信息](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
- [CA1707:标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
- [CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>请参阅

- [如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
