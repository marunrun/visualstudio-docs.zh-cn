---
title: 如何：创建或更新标准代码分析签入策略 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.policyeditor
helpviewer_keywords:
- code analysis, migrating check-in policy
ms.assetid: 458eb3b8-bb5e-4056-82b7-7079ce9c4089
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 47e7c2b6e02aab3b6b1df0c54ba91668bbb2673c
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825814"
---
# <a name="how-to-create-or-update-standard-code-analysis-check-in-policies"></a>如何：创建或更新标准代码分析签入策略
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以要求运行代码分析将对团队项目中的所有代码项目通过使用代码分析签入策略。 需要代码分析可以提高签入代码库的代码的质量。  
  
> [!NOTE]
> 仅当使用 Team Foundation Server 提供此功能。  
  
 代码分析签入策略设置在团队项目设置中，并将应用于团队项目中每个代码项目。 代码分析运行的代码项目的项目 (.xxproj) 文件中的代码项目的配置。 代码分析运行在本地计算机上执行。 时启用代码分析签入策略、 要签入代码项目中的文件必须在其最后一次编辑后编译和代码分析运行的最小值，包含团队项目设置中的规则必须在计算机上执行其中 changes 所做。  
  
- 通过指定的签入策略设置为托管代码中，*规则集*，其中包含代码分析规则的子集。  
  
- 对于 C /C++代码中，签入策略需要运行所有代码分析规则。 可以添加预处理器指令，以禁用你的团队项目中的单个代码项目的特定规则。  
  
  指定托管代码的签入策略后，团队成员可以同步到团队项目的策略设置的代码项目及其代码分析设置。  
  
### <a name="to-open-the-check-in-policy-editor"></a>若要打开签入策略编辑器  
  
1. 在团队资源管理器中右键单击团队项目名称，指向**团队项目设置**，然后单击**源代码管理**。  
  
2. 在中**源代码管理**对话框中，选择**签入策略**选项卡。  
  
3. 执行下列操作之一：  
  
    - 单击**添加**来创建新的签入策略。  
  
    - 双击现有**代码分析**中的项**策略类型**要更改的策略列表。  
  
### <a name="to-set-policy-options"></a>若要设置策略选项  
  
- 选中或清除以下选项：  
  
    |选项|描述|  
    |------------|-----------------|  
    |**执行签入以只包含属于当前解决方案的文件。**|只能对解决方案和项目配置文件中指定的文件，可以运行代码分析。 此策略可确保所有代码都是一种解决方案的一部分进行都分析。|  
    |**强制执行 C /C++代码分析 (/analyze)**|需要的所有 C 或C++项目在生成使用 /analyze 编译器选项，它们可以在签入之前运行代码分析。|  
    |**为托管代码强制实施代码分析**|需要托管的所有项目运行代码分析和生成它们可以在签入之前。|  
  
- 
  
### <a name="to-specify-a-managed-rule-set"></a>若要指定托管的规则设置  
  
- 从**运行此规则集**列出，请使用以下方法之一：  
  
  - 选择 Microsoft 标准规则集。  

  - 若要选择自定义规则集，请单击 **\<选择规则集从源代码管理...>** ，然后键入源代码管理浏览器中的规则集的版本控制路径。 版本控制路径的语法是：  

  - **$/** `TeamProjectName` **/** `VersionControlPath`  

  - 详细了解如何创建和实现自定义签入策略规则集，请参阅[为托管代码实施自定义签入策略](../code-quality/implementing-custom-code-analysis-check-in-policies-for-managed-code.md)。  
  
## <a name="see-also"></a>请参阅  
 [创建和使用代码分析签入策略](../code-quality/creating-and-using-code-analysis-check-in-policies.md)
