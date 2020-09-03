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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72609316"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果你必须使用不同版本的评估和创作代码分析签入策略 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] ，你必须了解如何 [!INCLUDE[vstsTfsOrcasLong](../includes/vststfsorcaslong-md.md)] 和 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 评估签入策略之间的差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>用于评估签入策略的版本兼容性

- 当在中计算代码分析签入策略时 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] ，中存在 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 但在中的任何规则 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 都将被忽略。

- 当在中计算代码分析签入策略时 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] ，将忽略所有独占的新规则 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 。

- 如果代码分析签入策略指定规则程序集， [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 则将忽略由它无法识别的程序集指定的所有规则。

- 如果代码分析签入策略指定了无法识别的规则程序集 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] ，则将显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作签入策略的版本兼容性

- 如果你使用的版本创建代码分析签入策略 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] ，则不能使用的 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 版本 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 来修改它。 而且， [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 不能评估策略。

- 如果你使用在中创建了代码分析签入策略 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] ， [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 则可以使用 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] 中的 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 修改它，还可以通过对策略进行评估 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 。 在中使用修改策略后 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] ，你将无法再使用中的来编辑该策略 [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 。 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 无需匹配强名称的问题即可评估策略。

- 若要使用适用于和的规则设置创建代码分析签入策略， [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 你必须在中创建策略 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] ，进行所需的所有更改并保存策略。 如果对规则所做的更改仅存在于中 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] ，则可以在中修改并保存策略 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] 。

     将策略保存到后 [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] ，你将无法再更改仅存在于中的规则的设置 [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] 。
