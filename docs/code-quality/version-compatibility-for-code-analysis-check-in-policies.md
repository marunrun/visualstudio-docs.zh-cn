---
title: 代码分析签入策略的版本兼容性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fc164dea10a74bbff725ee153f298c820f1c203
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825142"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性

如果您必须评估和编写代码分析签入策略使用不同版本的[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]，您必须知道方式间的差异[!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)]和[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]评估签入策略。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>版本兼容性评估签入策略

- 代码分析签入策略中的计算时[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]，在存在任何规则[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]中不存在，但[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]将被忽略。

- 代码分析签入策略中的计算时[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]，专用于的所有新规则[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]将被忽略。

- 如果代码分析签入策略指定规则程序集，[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]将忽略所指定的程序集，它无法识别的所有规则。

- 如果代码分析签入策略指定规则程序集的[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]无法识别，显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作签入策略的版本兼容性

- 如果您通过创建代码分析签入策略[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]新版[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]，不能使用[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]版本[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]对其进行修改。 同样，[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]无法评估策略。

- 如果您通过创建代码分析签入策略[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]中[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]，可以使用[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]中[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]若要修改它，并将策略可以还通过计算[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]。 通过使用修改的策略后[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]中[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]，不再可以通过编辑策略[!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]中[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 可以评估策略，而不会出现因不匹配的强名称而引起的问题。

- 若要创建具有两个应用的规则设置的代码分析签入策略[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]并[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]，必须创建中的策略[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]、 进行需要的所有更改和保存策略。 如果对规则的更改仅在存在[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]，修改并保存在策略[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]。

   保存中的策略后[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]，你无法再更改中存在的规则设置[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]仅。