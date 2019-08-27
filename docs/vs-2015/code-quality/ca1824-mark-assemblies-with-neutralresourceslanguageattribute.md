---
title: CA1824:用 NeutralResourcesLanguageAttribute 标记程序集 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 795d48b96392057a3f96cf3a67f3c49de8aee9b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203076"
---
# <a name="ca1824-mark-assemblies-with-neutralresourceslanguageattribute"></a>CA1824:用 NeutralResourcesLanguageAttribute 标记程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAssembliesWithNeutralResourcesLanguage|
|CheckId|CA1824|
|类别|Microsoft.Performance|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 程序集包含**ResX**-基于资源但不具有<xref:System.Resources.NeutralResourcesLanguageAttribute?displayProperty=fullName>应用于它。

## <a name="rule-description"></a>规则说明
 **NeutralResourcesLanguage**特性告知**ResourceManager**的语言，用于显示非特定区域性的资源的程序集。 在查找中作为非特定资源语言中，相同的区域性的资源时**ResourceManager**会自动使用位于主程序集中的资源。 而不是搜索具有当前线程的当前用户接口区域性的附属程序集执行此操作。 这将改进所加载的第一个资源的查找性能，并缩小工作集。

## <a name="fixing-violations"></a>解决冲突
 若要修复此规则的冲突，请将属性添加到该程序集，并指定非特定区域性的资源的语言。

## <a name="specifying-the-language"></a>指定的语言

#### <a name="to-specify-the-language-of-the-resource-of-the-neutral-culture"></a>若要指定非特定区域性的资源的语言

1. 在中**解决方案资源管理器**，右键单击你的项目，然后单击**属性**。

2. 从左侧的导航栏中选择**应用程序**，然后单击**程序集信息**。

3. 在中**程序集信息**对话框框中，选择从语言**中性语言**下拉列表。

4. 单击 **“确定”** 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它是允许要禁止显示此规则的警告。 但是，启动性能可能会降低。
