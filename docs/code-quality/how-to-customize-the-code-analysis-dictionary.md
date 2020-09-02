---
title: 如何：自定义代码分析字典
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1a50374a2603153cc7f4770a9aaf5ba72fbe007
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "87453647"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>如何：自定义代码分析字典

代码分析使用内置字典检查代码中的标识符，以了解 .NET 设计准则的拼写、语法用例和其他命名约定中的错误。 您可以创建自定义字典 Xml 文件，以添加、删除或修改内置字典的术语、缩写和首字母缩写词。

例如，假设代码包含一个名为 **DoorKnokker**的类。 代码分析会将名称标识为两个词的组合： **门** 和 **knokker**。 然后，它会发出警告，指出 **knokker** 拼写不正确。 若要强制代码分析识别拼写，可以将字词 **knokker** 添加到自定义字典中。

## <a name="to-create-a-custom-dictionary"></a>创建自定义字典

创建一个名为 **CustomDictionary.xml**的文件。

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

## <a name="custom-dictionary-elements"></a>自定义字典元素

您可以通过将字词作为以下元素的内部文本添加到自定义字典中来修改代码分析字典的行为：

- [字典/字词/识别/字](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [字典/字词/无法识别/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [字典/字词/弃用/字词 [ @PreferredAlternate ]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [字典/字词/复合/字词 [ @CompoundAlternate ]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [字典/字词/DiscreteExceptions/字词](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [字典/缩写词/CasingExceptions/缩写](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="dictionarywordsrecognizedword"></a><a name="BKMK_DictionaryWordsRecognizedWord"></a> 字典/字词/识别/字

若要在代码分析标识为正确拼写的字词列表中包括字词，请将该字词添加为字典/字词/识别/Word 元素的内部文本。 字典/字词/识别/Word 元素中的字词不区分大小写。

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

字典/字词/识别的节点中的字词适用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

- [CA2204:文字应正确拼写](../code-quality/ca2204.md)

### <a name="dictionarywordsunrecognizedword"></a><a name="BKMK_DictionaryWordsUnrecognizedWord"></a> 字典/字词/无法识别/Word

若要从代码分析标识为正确拼写的字词列表中排除字词，请添加要排除为字典/字词/无法识别/Word 元素的内部文本的字词。 字典/字词/无法识别/Word 元素中的词不区分大小写。

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

字典/字词/无法识别的节点中的字词应用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

- [CA2204:文字应正确拼写](../code-quality/ca2204.md)

### <a name="dictionarywordsdeprecatedtermpreferredalternate"></a><a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> 字典/字词/弃用/字词 [ @PreferredAlternate ]

若要在代码分析识别为不推荐使用的字词列表中包括字词，请将该字词添加为字典/字词/弃用/字词元素的内部文本。 弃用的字词是拼写正确但不应使用的单词。

若要在警告中包括建议的备用字词，请在 PreferredAlternate 属性中指定字词元素的备用项。 如果不想建议替代，则可以将属性值留空。

- 字典/字词/弃用/字词元素中的弃用字词不区分大小写。

- PreferredAlternate 特性值区分大小写。 将 Pascal 大小写用于复合备用。

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

字典/字词/弃用节点中的词条适用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

- [CA1726:使用首选词条](../code-quality/ca1726.md)

### <a name="dictionarywordscompoundtermcompoundalternate"></a><a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> 字典/字词/复合/字词 [ @CompoundAlternate ]

内置字典将一些字词标识为单个离散术语，而不是复合字词。 若要在代码分析识别为组合词并指定正确的字词大小写的字词列表中包括字词，请将该字词添加为字典/字词/复合/字词元素的内部文本。 在 Term 元素的 CompoundAlternate 属性中，通过将单个单词的第一个字母大写 (Pascal 大小写) ，指定构成复合字词的各个单词。 请注意，在内部文本中指定的术语会自动添加到 Dictionary/Words/DiscreteExceptions 列表中。

- 字典/字词/复合/字词元素中的复合字词不区分大小写。

- CompoundAlternate 特性值区分大小写。 将 Pascal 大小写用于复合备用。

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

字典/字词/复合节点中的词条适用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

- [CA1703:资源字符串应正确拼写](../code-quality/ca1703.md)

- [CA1704:标识符应正确拼写](../code-quality/ca1704.md)

### <a name="dictionarywordsdiscreteexceptionsterm"></a><a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> 字典/字词/DiscreteExceptions/字词

若要在由复合单词的大小写规则检查字词时，将代码分析识别为一个离散单词的字词列表中的字词，请将该字词添加为 Dictionary/Words/DiscreteExceptions/Term 元素的内部文本。 字典/字词/DiscreteExceptions/字词元素中的词不区分大小写。

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

字典/字词/DiscreteExceptions 节点中的字词适用于以下代码分析规则：

- [CA1701:资源字符串组合词应采用正确的大小写](../code-quality/ca1701.md)

- [CA1702:组合词应采用正确的大小写](../code-quality/ca1702.md)

### <a name="dictionaryacronymscasingexceptionsacronym"></a><a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> 字典/缩写词/CasingExceptions/缩写

若要在代码分析标识为正确拼写的字词列表中包含首字母缩写，并指示用复合词的大小写规则检查术语的首字母缩写，请将该词添加为字典/首字母缩写/CasingExceptions/缩写元素的内部文本。 字典/缩写词/CasingExceptions/缩写元素中的首字母缩写词区分大小写。

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

字典/首字母缩写/CasingExceptions 节点中的词条适用于以下代码分析规则：

- [CA1709:标识符的大小写应当正确](../code-quality/ca1709.md)

## <a name="to-apply-a-custom-dictionary-to-a-project"></a><a name="BKMK_ToApplyACustomDictionaryToAProject"></a> 向项目应用自定义字典

1. 在 **解决方案资源管理器**中，使用以下过程之一：

    - 若要将字典添加到单个项目中，请右键单击项目名称，然后单击 " **添加现有项**"。 在 " **添加现有项** " 对话框中指定该文件。
  
    - 若要添加两个或多个项目之间共享的字典，请在 " **添加现有项** " 对话框中找到要共享的文件，单击 " **添加** " 按钮上的向下箭头，然后单击 " **添加为链接**"。

2. 在 **解决方案资源管理器**中，右键单击 **CustomDictionary.xml** 的文件名，然后单击 " **属性**"。

3. 从 " **生成操作** " 列表中，选择 " **CodeAnalysisDictionary**"。

4. 从 " **复制到输出目录** " 列表中，选择 "不 **复制**"。
