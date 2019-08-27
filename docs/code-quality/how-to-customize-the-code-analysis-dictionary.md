---
title: 如何：自定义代码分析字典
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b43d731634022a2f3fcb9e00b552e75e5322db8c
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715235"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>如何：自定义代码分析字典

代码分析使用内置的字典来检查拼写、 语法的情况下和其他命名约定的.NET 设计准则中的错误代码中的标识符。 可以创建要添加、 删除或修改条款、 缩写和首字母缩写词到内置词典的自定义词典 Xml 文件。

例如，假设您的代码包含一个名为类**DoorKnokker**。 代码分析可以确定两个单词的复合的名称：**门**并**knokker**。 然后，它将引发一个警告， **knokker**拼写不正确。 若要强制代码分析，以识别拼写是否正确，可以添加字词**knokker**到自定义字典。

## <a name="to-create-a-custom-dictionary"></a>若要创建自定义词典

创建名为的文件**CustomDictionary.xml**。

使用以下 XML 结构定义自定义字词：

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>knokker</Word>
         </Unrecognized>
         <Recognized>
            <Word></Word>
         </Recognized>
         <Deprecated>
            <Term PreferredAlternate=""></Term>
         </Deprecated>
         <Compound>
            <Term CompoundAlternate=""></Term>
         </Compound>
         <DiscreteExceptions>
            <Term></Term>
         </DiscreteExceptions>
      </Words>
      <Acronyms>
         <CasingExceptions>
            <Acronym></Acronym>
         </CasingExceptions>
      </Acronyms>
   </Dictionary>
```

## <a name="custom-dictionary-elements"></a>自定义词典元素

可以通过将条款添加为自定义字典中的以下元素的内部文本来修改代码分析字典中的行为：

- [字典/单词/识别/中的单词](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [字典/单词/无法识别的/中的单词](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [Dictionary/Words/Deprecated/Term[@PreferredAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [Dictionary/Words/Compound/Term[@CompoundAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [Dictionary/Acronyms/CasingExceptions/Acronym](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="BKMK_DictionaryWordsRecognizedWord"></a> 字典/单词/识别/中的单词

若要包括的代码分析会正确标识的字词列表中的一个术语，拼写，作为字典/单词/识别/Word 元素的内部文本添加术语。 字典/单词/识别/Word 元素中的条款不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Recognized>
            <Word>knokker</Word>
            ...
         </Recognized>
         ...
      </Words>
      ...
</Dictionary>
```

字典/单词/识别节点中的条款被应用于以下的代码分析规则：

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204:应正确拼写文本](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsUnrecognizedWord"></a> 字典/单词/无法识别的/中的单词

若要从代码分析可确定会正确拼写的术语的列表中排除一个术语，添加要作为字典/单词/无法识别/Word 元素的内部文本中排除的术语。 字典/单词/无法识别/Word 元素中的条款不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>meth</Word>
            ...
         </Unrecognized>
         ...
      </Words>
      ...
</Dictionary>
```

无法识别的单词/字典/节点中的条款被应用于以下的代码分析规则：

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

- [CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)

- [CA2204:应正确拼写文本](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> Dictionary/Words/Deprecated/Term[@PreferredAlternate]

若要在代码分析可确定为不推荐使用的术语列表中包含一个术语，将添加为字典/单词/已弃用/术语元素的内部文本的一词。 不推荐使用的术语是一个单词的拼写正确，但不应使用。

若要包含在警告中建议的替代字词，字词元素 PreferredAlternate 属性中指定备用服务器。 如果不希望建议一个替代，可以将属性值留空。

- 字典/单词中的不推荐使用的词条/已弃用/术语元素不是区分大小写。

- PreferredAlternate 属性值是区分大小写。 对于复合备用项使用 Pascal 大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Deprecated>
            <Term PreferredAlternate="LogOn">login</Term>
            ...
         </Deprecated>
         ...
      </Words>
      ...
</Dictionary>
```

已弃用的单词/字典/节点中的条款被应用于以下的代码分析规则：

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

- [CA1726:使用首选的词条](../code-quality/ca1726-use-preferred-terms.md)

### <a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> Dictionary/Words/Compound/Term[@CompoundAlternate]

内置词典标识作为单一的离散的术语，而不是一个复合术语的一些术语。 若要与搜索条件的代码分析标识为一个组合词列表中包括一个术语，并指定正确的大小写的字词，添加一词作为字典/单词/复合/术语元素的内部文本。 术语元素 CompoundAlternate 属性中指定的单个单词利用不同的单词 （Pascal 大小写） 的第一个字母组成的复合术语。 请注意，内部文本中指定的术语自动添加到字典/单词/DiscreteExceptions 列表。

- 字典/单词中的不推荐使用的词条/已弃用/术语元素不是区分大小写。

- PreferredAlternate 属性值是区分大小写。 对于复合备用项使用 Pascal 大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <Compound>
            <Term CompoundAlternate="CheckBox">checkbox</Term>
            ...
         </Compound>
         ...
      </Words>
      ...
</Dictionary>
```

字典/单词/化合物节点中的条款被应用于以下的代码分析规则：

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

### <a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> 字典/单词/DiscreteExceptions/术语

若要排除的代码分析作为单个标识的字词列表中的字词，离散 word 字词被选中的组合词的大小写规则时，将添加为字典/单词/DiscreteExceptions/术语元素的内部文本的术语。 字典/单词/DiscreteExceptions/术语元素中的字词不区分大小写。

**示例**

```xml
<Dictionary>
      <Words>
         <DiscreteExceptions>
            <Term>checkbox</Term>
            ...
         </DiscreteExceptions>
         ...
      </Words>
      ...
</Dictionary>
```

字典/单词/DiscreteExceptions 节点中的条款被应用于以下的代码分析规则：

- [CA1701:资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)

- [CA1702:复合词应采用正确的大小写](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

### <a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Dictionary/Acronyms/CasingExceptions/Acronym

中的代码分析将标识为拼写正确的字词列表包括首字母缩略词并指示如何的首字母缩写词大小写被选中时规则的组合词，将字词添加为字典/首字母缩写词/CasingExceptions 的内部文本 /首字母缩略词元素。 字典/首字母缩写词/CasingExceptions/首字母缩略词元素中的首字母缩写是区分大小写。

**示例**

```xml
<Dictionary>
      <Acronyms>
         <CasingExceptions>
            <Acronym>NESW</Acronym>   <!-- North East South West -->
            ...
         </CasingExceptions>
         ...
      </Acronyms>
      ...
</Dictionary>
```

字典/首字母缩写词/CasingExceptions 节点中的条款被应用于以下的代码分析规则：

- [CA1709:标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

## <a name="BKMK_ToApplyACustomDictionaryToAProject"></a> 若要应用于项目的自定义词典

1. 在中**解决方案资源管理器**，使用以下过程之一：

2. 要将字典添加到单个项目中，右键单击项目名称，然后单击**添加现有项**。 指定的文件中**添加现有项**对话框。

3. 若要添加一个字典，其中在两个或多个项目间共享，请找到共享中的文件**添加现有项**对话框框中，单击向下箭头**添加**按钮，然后单击**添加为链接**.

4. 在中**解决方案资源管理器**，右键单击**CustomDictionary.xml**文件名称，然后单击**属性**。

5. 从**生成操作**列表中，选择**CodeAnalysisDictionary**。

6. 从**复制到输出目录**列表中，选择**不要复制**。