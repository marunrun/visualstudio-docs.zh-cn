---
title: 代码分析应用程序错误
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio ALM], code analysis
- code analysis, errors
- managed code, code analysis errors
- code analysis, policy errors
ms.assetid: d8fd9475-ac9b-4085-b5a3-b0c807922cac
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ef5ccc0cf432a5c6782b76c4623bfdc55f66a8b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538550"
---
# <a name="code-analysis-application-errors"></a>代码分析应用程序错误
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
本部分是托管代码分析工具生成的错误消息的引用。 若要获取特定错误消息的相关帮助，请在索引的 " **查找** " 框中键入错误号。

## <a name="in-this-section"></a>本节内容

|项|值|
|-|-|
|[CA0001](ca0001.md)|托管代码分析工具中引发了异常，但未指示预期的错误条件。|
|[CA0051](ca0051.md)|未选择任何规则。|
|[CA0052](ca0052.md)|未选择要分析的目标。|
|[CA0053](ca0053.md)|无法加载规则程序集。|
|[CA0054](ca0054.md)|自定义规则程序集具有无效的 XML 资源。|
|[CA0055](ca0055.md)|无法加载文件：\<path>|
|[CA0056](ca0056.md)|项目文件的版本不正确。|
|[CA0057](ca0057.md)|不能将冲突映射到当前目标和规则集。|
|[CA0058](ca0058.md)|无法加载引用的程序集。|
|[CA0059](ca0059.md)|命令行开关错误。|
|[CA0060](ca0060.md)|无法加载间接引用的程序集。|
|[CA0061](ca0061.md)|未能找到规则 "*RuleId*"。|
|[CA0062](ca0062.md)|未能找到规则集 "*RuleSetName*" 中引用的规则 "*RuleId*"。|
|[CA0063](ca0063.md)|未能加载规则集文件或其从属规则集文件之一。|
|[CA0064](ca0064.md)|未执行任何分析，因为指定的规则集不包含任何 FxCop 规则。|
|[CA0065](ca0065.md)|不支持的元数据构造：类型 "*TypeName*" 同时包含具有相同名称 "*PropertyFieldName*" 的属性和字段|
|[CA0066](ca0066.md)|为 **/targetframeworkversion**提供的值 "*VersionID*" 不是已识别的版本。|
|[CA0067](ca0067.md)|找不到目录。|
|[CA0068](ca0068.md)|找不到目标程序集 *"AssemblyName"* 的调试信息。|
|[CA0069](ca0069.md)|使用备用平台。 找不到*FrameworkVersion1* 。 改为使用 *FrameworkVersion2* 。 为获得最佳分析结果，请确保安装了正确的 .NET Framework。|
|[CA0070](ca0070.md)|由于安全权限的原因，无法加载程序集或类型。|
|[CA0501](ca0501.md)|无法读取输出报告。|
|[CA0502](ca0502.md)|语言不受支持。|
|[CA0503](ca0503.md)|属性已弃用。 使用 superceding 属性|
|[CA0504](ca0504.md)|已忽略规则目录，因为它不存在|
|[CA0505](ca0505.md)|属性已弃用。 使用 superceding 属性|
|[FxCopCmd 错误](fxcopcmd-errors.md)|托管代码分析错误。|

## <a name="related-sections"></a>相关章节

- [编写安全代码的准则](https://msdn.microsoft.com/9892fd19-45cd-44b6-9fa8-10f1b5cb6ea4)
- [分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)
- [用于排除 Application Lifecycle Management 工具错误的资源](https://msdn.microsoft.com/library/76ca8f76-1e2d-4b55-89e2-bd59e4abe74c)