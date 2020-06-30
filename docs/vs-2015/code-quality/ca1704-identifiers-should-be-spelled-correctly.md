---
title: CA1704：标识符应正确拼写 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
helpviewer_keywords:
- CA1704
- IdentifiersShouldBeSpelledCorrectly
ms.assetid: f2c7a44d-1690-44ca-9cd0-681b04b12b2a
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b5e078fc1bb7fe247d541e7695e98c2de76c2466
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544061"
---
# <a name="ca1704-identifiers-should-be-spelled-correctly"></a>CA1704:标识符应正确拼写
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|IdentifiersShouldBeSpelledCorrectly|
|CheckId|CA1704|
|Category|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符的名称包含一个或多个未被 Microsoft 拼写检查器库识别的单词。 此规则不检查构造函数或特殊命名成员，如 get 和 set 属性访问器。

## <a name="rule-description"></a>规则描述
 此规则将标识符分析为标记，并检查每个标记的拼写。 分析算法执行以下转换：

- 大写字母开始新令牌。 例如，将 MyNameIsJoe 切分为 "My"、"Name"、"Is" 和 "Joe"。

- 对于多个大写字母，最后一个大写字母会开始一个新的标记。 例如，GUIEditor 切分到 "GUI"，"Editor"。

- 删除前导和尾随撇号。 例如，发件人 "切分"。

- 下划线表示标记的末尾并被删除。 例如，Hello_world 切分为 "Hello"，"world"。

- 删除嵌入的符号。 例如，对于&切分 "设置为" format "。

  默认情况下，使用英语（en）版本的拼写检查器。 当前没有其他语言词典可用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更正单词的拼写，或将该词添加到名为 CustomDictionary.xml 的自定义字典中。 将字典放置在工具的安装目录、项目目录或与用户配置文件（%USERPROFILE%\Application Data ...）下的工具关联的目录中 \\ 。若要了解如何将自定义字典添加到中的项目 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，请参阅[如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)

- 添加不应在字典/字词/识别路径下产生冲突的单词。

- 添加应在字典/字词/无法识别的路径下引发冲突的单词。

- 添加在字典/字词/弃用路径下应标记为过时的字词。 有关详细信息，请参阅相关规则主题[CA1726：使用首选字词](../code-quality/ca1726-use-preferred-terms.md)。

- 将例外项大小写规则添加到字典/缩写词/CasingExceptions 路径中。

  下面是自定义字典文件结构的示例。

```
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
 仅当 word 有意拼写错误，并且 word 适用于有限的库集时，才禁止显示此规则发出的警告。 拼写正确的单词可减少新软件库所需的学习曲线。

## <a name="related-rules"></a>相关规则
 [CA2204:文字应正确拼写](../code-quality/ca2204-literals-should-be-spelled-correctly.md)

 [CA1703:资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)

 [CA1709:标识符的大小写应当正确](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708:标识符应以大小写之外的差别进行区分](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707:标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1726:使用首选词条](../code-quality/ca1726-use-preferred-terms.md)

## <a name="see-also"></a>另请参阅
 [如何：自定义代码分析字典](../code-quality/how-to-customize-the-code-analysis-dictionary.md)
