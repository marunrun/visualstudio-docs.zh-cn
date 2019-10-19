---
title: 代码分析签入策略的版本兼容性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 075981569cbee05e90afe17b3afc9558d7bbb270
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609316"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你必须使用 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 的不同版本来评估和创作代码分析签入策略，你必须知道 [!INCLUDE[vstsTfsOrcasLong](../includes/vststfsorcaslong-md.md)] 和 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 评估签入策略的方式之间的差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>用于评估签入策略的版本兼容性

- 在 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中评估代码分析签入策略时，将忽略 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中存在但在 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中不存在的任何规则。

- 在 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中评估代码分析签入策略时，将忽略所有专用于 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 的新规则。

- 如果代码分析签入策略指定规则程序集，[!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 将忽略由它无法识别的程序集指定的所有规则。

- 如果代码分析签入策略指定 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 无法识别的规则程序集，则将显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作签入策略的版本兼容性

- 如果使用 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 的 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 版本创建代码分析签入策略，则不能使用 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 的 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 版本来修改它。 而且，[!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 无法评估策略。

- 如果在 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中使用 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 创建了代码分析签入策略，则可以使用 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中的 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 来修改该策略，也可以通过 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 来评估该策略。 使用 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中的 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 修改策略后，你将无法再使用 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中的 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 来编辑该策略。 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 可以评估策略，而不会出现因不匹配的强名称而引起的问题。

- 若要创建同时适用于 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 和 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 的规则设置的代码分析签入策略，你必须在 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中创建策略，进行所需的所有更改，并保存策略。 如果对规则所做的更改仅在 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中存在，则在 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中修改并保存策略。

     在 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 中保存策略后，你将无法再更改仅存在于 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 中的规则的设置。
