---
title: CA1824：用 NeutralResourcesLanguageAttribute 标记程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1824
- MarkAssembliesWithNeutralResourcesLanguage
helpviewer_keywords:
- MarkAssembliesWithNeutralResourcesLanguage
- CA1824
ms.assetid: 10e97f8a-aa6e-47aa-b253-1e5d3a295d82
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 19077a63d5aa22bda3f968943703a82488e2745d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545283"
---
# <a name="ca1824-mark-assemblies-with-neutralresourceslanguageattribute"></a>CA1824:用 NeutralResourcesLanguageAttribute 标记程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|类别|Microsoft. 性能|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 程序集包含基于**ResX**的资源，但没有 <xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName> 应用到它。

## <a name="rule-description"></a>规则描述
 **NeutralResourcesLanguage**特性通知用于显示程序集的非特定区域性资源的语言的**ResourceManager** 。 当它在与非特定区域性资源语言相同的区域性中查找资源时， **ResourceManager**会自动使用位于主程序集中的资源。 它不会搜索具有当前线程的当前用户界面区域性的附属程序集。 这将改进所加载的第一个资源的查找性能，并缩小工作集。

## <a name="fixing-violations"></a>解决冲突
 若要修复与此规则的冲突，请将属性添加到程序集，并指定非特定区域性的资源的语言。

## <a name="specifying-the-language"></a>指定语言

#### <a name="to-specify-the-language-of-the-resource-of-the-neutral-culture"></a>指定非特定区域性的资源的语言

1. 在**解决方案资源管理器**中，右键单击你的项目，然后单击 "**属性**"。

2. 从左侧导航栏中选择 "**应用程序**"，然后单击 "**程序集信息**"。

3. 在 "**程序集信息**" 对话框中，从 "**非特定语言**" 下拉列表中选择语言。

4. 单击 **“确定”** 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 允许禁止显示此规则发出的警告。 但是，启动性能可能会降低。
