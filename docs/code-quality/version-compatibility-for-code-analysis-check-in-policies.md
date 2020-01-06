---
title: 代码分析签入策略的版本兼容性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4757b3a105ff02a92944d9b45e645e2c63a8b81c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587155"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性

如果你必须使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]的不同版本来评估和创作代码分析签入策略，你必须知道 [!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] 和 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 评估签入策略的方式之间的差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>用于评估签入策略的版本兼容性

- 在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]中评估代码分析签入策略时，将忽略 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中存在但在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中不存在的任何规则。

- 在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]中评估代码分析签入策略时，将忽略所有专用于 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 的新规则。

- 如果代码分析签入策略指定规则程序集，[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 将忽略由它无法识别的程序集指定的所有规则。

- 如果代码分析签入策略指定 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无法识别的规则程序集，则将显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作签入策略的版本兼容性

- 如果使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)]的 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 版本创建代码分析签入策略，则不能使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 的 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 版本来修改它。 而且，[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无法评估策略。

- 如果在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]中使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 创建了代码分析签入策略，则可以使用 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 来修改该策略，也可以通过 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]来评估该策略。 使用 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 修改策略后，你将无法再使用 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 来编辑该策略。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 可以在不匹配强名称的情况下评估策略。

- 若要创建同时适用于 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 和 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]的规则设置的代码分析签入策略，你必须在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)]中创建策略，进行所需的所有更改，并保存策略。 如果对规则所做的更改仅在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]中存在，则在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]中修改并保存策略。

   在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)]中保存策略后，你将无法再更改仅存在于 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中的规则的设置。
