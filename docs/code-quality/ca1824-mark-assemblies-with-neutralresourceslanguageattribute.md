---
title: CA1824:用 NeutralResourcesLanguageAttribute 标记程序集
ms.date: 03/29/2018
ms.topic: reference
f1_keywords:
- CA1824
- MarkAssembliesWithNeutralResourcesLanguage
helpviewer_keywords:
- MarkAssembliesWithNeutralResourcesLanguage
- CA1824
ms.assetid: 10e97f8a-aa6e-47aa-b253-1e5d3a295d82
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40cb2a3674884a9fb4f1449c9afa2e0a2d27050f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62808555"
---
# <a name="ca1824-mark-assemblies-with-neutralresourceslanguageattribute"></a>CA1824:用 NeutralResourcesLanguageAttribute 标记程序集

|||
|-|-|
|TypeName|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因

程序集包含**ResX**-基于资源但不具有<xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName>应用于它。

## <a name="rule-description"></a>规则说明

<xref:System.Resources.NeutralResourcesLanguageAttribute>属性会通知应用程序的默认区域性的资源管理器。 如果默认区域性的资源嵌入到应用的主程序集，并<xref:System.Resources.ResourceManager>必须检索属于相同的区域性的默认区域性资源<xref:System.Resources.ResourceManager>会自动使用位于主程序集中的资源而不是搜索附属程序集。 这会绕过常用的程序集探测，提高了加载，并可以减少您的工作集的第一个资源的查找性能。

> [!TIP]
> 请参阅[打包和部署资源](/dotnet/framework/resources/packaging-and-deploying-resources-in-desktop-apps)进程的<xref:System.Resources.ResourceManager>用来探测资源文件。

## <a name="fix-violations"></a>修复冲突

若要修复此规则的冲突，请将属性添加到该程序集，并指定非特定区域性的资源的语言。

### <a name="to-specify-the-neutral-language-for-resources"></a>若要指定资源的非特定语言

1. 在中**解决方案资源管理器**，右键单击项目，并选择**属性**。

2. 选择**应用程序**选项卡，然后选择**程序集信息**。

   > [!NOTE]
   > 如果你的项目的标准.NET 或.NET Core 项目，请选择**包**选项卡。

3. 选择的语言从**非特定语言**或**程序集的非特定语言**下拉列表。

4. 选择 **确定**。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它是允许要禁止显示此规则的警告。 但是，启动性能可能会降低。

## <a name="see-also"></a>请参阅

- <xref:System.Resources.NeutralResourcesLanguageAttribute>
- [桌面应用 (.NET) 中的资源](/dotnet/framework/resources/)
- [CA1703-资源字符串应正确拼写](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
- [CA1701-资源字符串复合词应采用正确的大小写](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)