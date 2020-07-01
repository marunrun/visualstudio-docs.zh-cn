---
title: CA2210：程序集应具有有效的强名称 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8f800a550717abfabdfb9296fc8f6de49d127d73
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548195"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210:程序集应具有有效的强名称
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AssembliesShouldHaveValidStrongNames|
|CheckId|CA2210|
|Category|Microsoft. Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 没有使用强名称对程序集进行签名，无法验证强名称，或者如果没有计算机的当前注册表设置，则强名称将无效。

## <a name="rule-description"></a>规则描述
 此规则检索并验证程序集的强名称。 如果满足以下任一条件，则会发生冲突：

- 程序集没有强名称。

- 在签名后更改了程序集。

- 该程序集是延迟签名的。

- 程序集的签名不正确，或签名失败。

- 程序集要求注册表设置通过验证。 例如，使用强名称工具（Sn.exe）跳过对该程序集的验证。

  强名称可避免客户端在不知情的情况下加载已被篡改的程序集。 除非极为有限的几种情况，否则不应部署没有强名称的程序集。 如果共享或发布未正确签名的程序集，则该程序集可能被篡改，公共语言运行时可能不会加载该程序集；而用户可能必须在他/她的计算机上禁用验证。 没有强名称的程序集具有以下缺点：

- 无法验证其来源。

- 如果更改了程序集的内容，则公共语言运行时无法警告用户。

- 不能将其加载到全局程序集缓存中。

  请注意，若要加载和分析延迟签名的程序集，您必须对程序集禁用验证。

## <a name="how-to-fix-violations"></a>如何解决冲突
 **创建密钥文件**

 可使用下列过程之一：

- 使用 SDK 提供的程序集链接器工具（Al.exe） [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

- 对于 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 1.0 或1.1 版，使用 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> 或 <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName> 属性。

- 对于 [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] ，使用 `/keyfile` `/keycontainer` c + + 中的或编译器选项[/KEYFILE （指定密钥或密钥对来对程序集进行签名](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06)）或[/KEYCONTAINER （指定密钥容器来为程序集签名）](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e)链接器选项。

  **在 Visual Studio 中使用强名称对程序集进行签名**

1. 在中 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ，打开解决方案。

2. 在**解决方案资源管理器**中，右键单击你的项目，然后单击 "**属性"。**

3. 单击 "**签名**" 选项卡，然后选中 "为**程序集签名**" 复选框。

4. 从 "**选择强名称密钥文件**" 中，选择 "**新建**"。

    将显示 "**创建强名称密钥**" 窗口。

5. 在 "**密钥文件名称**" 中，键入强名称密钥的名称。

6. 选择是否使用密码来保护密钥，然后单击 **"确定"**。

7. 在**解决方案资源管理器**中，右键单击你的项目，然后单击 "**生成**"。

   **在 Visual Studio 外部使用强名称对程序集进行签名**

- 使用 SDK 提供的强名称工具（Sn.exe） [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。 有关详细信息，请参阅[Sn.exe （强名称工具）](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 仅当程序集用于不考虑篡改内容的环境中时，才禁止显示此规则发出的警告。

## <a name="see-also"></a>另请参阅
 <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName> <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
 [如何：使用强名称为程序集签名](https://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67) [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/c1d2b532-1b8e-4c7a-8ac5-53b801135ec6)
