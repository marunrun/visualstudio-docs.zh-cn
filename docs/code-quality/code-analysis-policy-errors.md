---
title: 代码分析策略错误
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.policyfailures
helpviewer_keywords:
- policy errors, code analysis
ms.assetid: d1f221cd-68c0-4277-9397-b76ad0dbae77
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 661f029b617c430f7205552080a94affc5bd543b
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72445886"
---
# <a name="code-analysis-policy-errors"></a>代码分析策略错误

如果签入时未满足代码分析策略，则会发生以下错误：

**一个或多个项目的代码分析设置与代码分析策略不兼容。**

对于一个或多个代码项目，代码分析要求签入到项目源代码管理中。 此错误可能是由以下一种或多种情况引起的：

- 未对解决方案中所有项目的生成版本启用代码分析。

- Visual Studio 中项目的本地规则集的**操作**设置限制低于项目规则集，例如，服务器上设置为 "**操作**=**错误**" 的规则将其 "**操作**" 设置为 "**警告**" 或在 Visual Studio 中运行的规则集中**没有**。

- 在 Visual Studio 中指定的规则集不包含在项目的代码分析签入策略中指定的规则集中指定的所有规则。

**代码分析策略失败。项目 {0} 中有错误，或生成不是最新的。**

生成包含错误或修复了错误，但修复后未执行代码分析。

**签入失败。代码分析策略要求使用打开的解决方案通过 Visual Studio 签入。**

代码分析策略要求签入的所有文件必须位于当前打开的解决方案中。 若要更正此错误，请打开包含要签入的文件的解决方案。

**并非挂起签入中的所有文件都在当前打开的解决方案中。**

代码分析策略要求签入的所有文件必须位于当前打开的解决方案中。 当存在打开的解决方案，但 "挂起签入" 视图中的某些文件不是当前打开的解决方案的一部分时，将引发此错误。 若要更正此错误，请打开包含要签入的文件的解决方案。

**"@No__t_1" 的版本不正确。策略中指定的强名称为 "{1}"。**

此错误适用于 .NET 项目。 代码分析策略所需的规则 .dll 存在于本地计算机上，但版本/公钥不匹配。 若要更正此错误，策略创建者必须在其计算机上更新*C:\Program Files\Microsoft Visual Studio 8 \ Team Tools\Static Analysis \\ Tools\FxCop\Rules*中的 .dll。

**策略中指定的 "{0}" 程序集不存在。**

此错误适用于 .NET 项目。 代码分析策略所需的规则未在客户端计算机上安装相应的 dll。 若要更正此错误，策略创建者必须在其计算机上更新*C:\Program Files\Microsoft Visual Studio 8 \ Team Tools\Static Analysis Tools\FxCop\Rules \\* 目录中的 dll。

**项目 {0} 规则设置与代码分析策略不一致。**

此错误适用于 .NET 项目。 托管代码规则设置与策略要求并不严格。 若要更正此错误，客户端设置必须与服务器上的策略要求相同或更严格。

**在活动配置上未启用代码分析。签入之前，切换到配置 {0} 并生成项目 {1}。**

在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，活动配置未启用代码分析，但至少启用了一个代码分析。

**在签入之前，必须在项目 {0} 属性中启用托管二进制文件的代码分析和生成。**

此错误适用于 .NET 应用程序 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]。 策略需要执行托管代码分析，但不会在客户端上的当前项目中启用它。

**签入之前，必须在项目 {0} 属性和生成中启用代码分析。**

此错误应用到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目和 web 项目。 策略需要执行托管代码分析，但不会在客户端上的当前项目中启用它。

**签入之前，必须C++在项目 {0} 属性和生成中启用 C/代码分析。**

此错误适用于非托管项目。 代码分析策略需要适用于 C/C++的代码分析，但在客户端上的当前项目中未启用。

## <a name="see-also"></a>请参阅

- [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)
