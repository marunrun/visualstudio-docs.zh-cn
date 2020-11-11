---
title: 代码分析签入策略的版本兼容性
ms.date: 11/04/2016
description: 了解团队系统 2008 Team Foundation Server 和 Team Foundation Server 2010 以不同的方式评估 Visual Studio 签入策略。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 3a681f510da270bc22ae4bc983103f9a5735a127
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436870"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性

如果你必须使用不同版本的评估和创作代码分析签入策略 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] ，你必须了解如何 [!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] 和 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 评估签入策略之间的差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>用于评估 Check-In 策略的版本兼容性

- 当在中计算代码分析签入策略时 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ，中存在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 但在中的任何规则 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 都将被忽略。

- 当在中计算代码分析签入策略时 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ，将忽略所有独占的新规则 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 。

- 如果代码分析签入策略指定规则程序集， [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 则将忽略由它无法识别的程序集指定的所有规则。

- 如果代码分析签入策略指定了无法识别的规则程序集 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ，则将显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>用于创作 Check-In 策略的版本兼容性

- 如果你使用的版本创建代码分析签入策略 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] ，则不能使用的 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 版本 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 来修改它。 而且， [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 不能评估策略。

- 如果你使用在中创建了代码分析签入策略 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] ， [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 则可以使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 中的 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 修改它，还可以通过对策略进行评估 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 。 在中使用修改策略后 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ，你将无法再使用中的来编辑该策略 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无需匹配强名称的问题即可评估策略。

- 若要使用适用于和的规则设置创建代码分析签入策略， [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 你必须在中创建策略 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ，进行所需的所有更改并保存策略。 如果对规则所做的更改仅存在于中 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ，则可以在中修改并保存策略 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 。

   将策略保存到后 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ，你将无法再更改仅存在于中的规则的设置 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 。
