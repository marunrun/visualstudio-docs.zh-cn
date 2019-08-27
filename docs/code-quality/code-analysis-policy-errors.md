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
ms.openlocfilehash: 103a48172665875c3615ce57b90dc77beeb6b5c4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806298"
---
# <a name="code-analysis-policy-errors"></a>代码分析策略错误

如果在签入时未满足代码分析策略，会发生以下错误：

**一个或多个项目的代码分析设置不兼容与代码分析策略。**

一个或多个代码项目不符合在签入到源代码管理项目的代码分析需求。 此错误可能是由以下一种或多种情况引起的：

- 未对解决方案中所有项目的生成版本启用代码分析。

- 本地规则集 for Visual Studio 中的项目的限制更少**操作**设置不是项目规则等设置的规则，设置为**操作**=**错误**服务器上具有其**操作**设置为**警告**或**无**中设置要在 Visual Studio 中运行的规则)。

- 在 Visual Studio 中指定的规则集不包含所有设置中的代码分析签入策略项目指定规则中指定的规则。

**代码分析策略失败。在项目中有错误{0}或生成不是最新。**

可以生成包含错误或已修复错误，但修复后没有执行过代码分析。

**签入失败。代码分析策略要求，在签入通过 Visual Studio 打开一个解决方案。**

代码分析策略要求签入的所有文件都必须位于当前打开的解决方案。 若要更正此错误，请打开包含要签入的文件的解决方案。

**在挂起的签入中的所有文件都处于当前打开的解决方案中。**

代码分析策略要求签入的所有文件都必须位于当前打开的解决方案。 当打开的解决方案，但"挂起签入"视图中的某些文件不是当前打开的解决方案的一部分时，会引发此错误。 若要更正此错误，请打开包含要签入的文件的解决方案。

**版本{0}不正确。强名称的策略中指定为{1}。**

此错误适用于.NET 项目。 在本地计算机上存在所需的代码分析策略规则.dll 但版本/公钥不匹配。 若要更正此错误，策略创建者必须更新在.dll *C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules\\* 目录在其计算机上。

**{0}的策略中指定的程序集不存在。**

此错误适用于.NET 项目。 所需的代码分析策略的规则没有相应的客户端计算机上安装的 dll。 若要更正此错误，策略创建者必须更新中的 dll *C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules\\* 目录在其计算机上。

**项目{0}规则设置不是使用代码分析策略的符合性。**

此错误适用于.NET 项目。 托管的代码规则设置不严格的策略要求。 若要更正此错误，客户端设置必须相同或比在服务器上的策略要求更严格。

**活动配置上未启用代码分析。切换到的配置{0}并生成项目{1}之前签入。**

在[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]、 活动配置中不包含启用代码分析，但没有启用的至少一种代码分析。

**必须在项目中的托管二进制文件启用代码分析{0}属性和之前的版本签入。**

此错误适用于[!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)].NET 应用程序。 该策略需要托管的代码分析，以执行，但未启用客户端上的当前项目中。

**必须在项目中启用代码分析{0}属性和之前的版本签入。**

应用于此错误[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]项目和 web 项目。 该策略需要托管的代码分析，以执行，但未启用客户端上的当前项目中。

**必须启用 C /C++项目中的代码分析{0}属性和之前的版本签入。**

此错误适用于非托管项目。 代码分析策略要求代码分析 c /C++，但它未启用客户端上的当前项目中。

## <a name="see-also"></a>请参阅

- [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)