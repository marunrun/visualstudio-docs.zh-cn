---
title: CA2210:程序集应具有有效的强名称 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f94183c6051ed0c2603bbfe35484fabb83a2160f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697990"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210:程序集应具有有效的强名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|类别|Microsoft.Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 未使用强名称签名程序集无法验证强名称，或强名称是无当前计算机的注册表设置无效。

## <a name="rule-description"></a>规则说明
 此规则检索并验证程序集的强名称。 如果以下任何条件成立，则会发生冲突：

- 程序集没有强名称。

- 登录后，该程序集已被更改。

- 程序集进行延迟签名。

- 程序集的签名错误，或签名失败。

- 程序集需要注册表设置，通过验证。 例如，使用强名称工具 (Sn.exe) 要跳过验证的程序集。

  强名称可避免客户端在不知情的情况下加载已被篡改的程序集。 除非极为有限的几种情况，否则不应部署没有强名称的程序集。 如果共享或发布未正确签名的程序集，则该程序集可能被篡改，公共语言运行时可能不会加载该程序集；而用户可能必须在他/她的计算机上禁用验证。 没有强名称程序集具有以下缺点：

- 无法验证其来源。

- 公共语言运行时不能发出警告用户如果已更改的程序集的内容。

- 它不能加载到全局程序集缓存。

  请注意，如果要加载和分析延迟签名程序集，必须先禁用该程序集的验证。

## <a name="how-to-fix-violations"></a>如何解决冲突
 **若要创建密钥文件**

 使用以下过程之一：

- 使用提供的程序集链接器工具 (Al.exe) [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK。

- 有关[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]v1.0 或 v1.1，使用<xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>或<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>属性。

- 有关[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]，可以使用两种`/keyfile`或`/keycontainer`编译器选项[/KEYFILE （指定密钥或密钥对以便为程序集签名）](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06)或[/KEYCONTAINER （指定密钥容器以便为程序集签名）](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e)中的链接器选项C++)。

  **若要对 Visual Studio 中的强名称程序集签名**

1. 在[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，打开你的解决方案。

2. 在中**解决方案资源管理器**，右键单击项目，然后单击**属性。**

3. 单击**签名**选项卡，然后选择**程序集签名**复选框。

4. 从**选择强名称密钥文件**，选择**新建**。

    **创建强名称密钥**窗口将显示。

5. 在中**密钥文件名称**，键入强名称密钥的名称。

6. 选择是否要使用密码保护密钥，然后单击**确定**。

7. 在中**解决方案资源管理器**，右键单击项目，然后单击**生成**。

   **若要对使用 Visual Studio 外部强名称程序集签名**

- 使用提供的强名称工具 (Sn.exe) [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK。 有关详细信息，请参阅 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果在环境中使用该程序集，则仅禁止显示此规则的警告的篡改内容并不是问题。

## <a name="see-also"></a>请参阅
 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
 [如何：使用强名称为程序集签名](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67) [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)
