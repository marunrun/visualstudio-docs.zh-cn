---
title: CA2210:程序集应具有有效的强名称
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
helpviewer_keywords:
- AssembliesShouldHaveValidStrongNames
- CA2210
ms.assetid: 8ed33d1c-8ec6-4b47-a692-e22dc8693088
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89edba30a95d61268aebb26de8d973f6201c0fcf
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714762"
---
# <a name="ca2210-assemblies-should-have-valid-strong-names"></a>CA2210:程序集应具有有效的强名称

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

### <a name="create-a-key-file"></a>创建密钥文件

使用以下过程之一：

- 使用[程序集链接器工具 (Al.exe)](/dotnet/framework/tools/al-exe-assembly-linker)。

- 对于.NET Framework 2.0 中，使用`/keyfile`或`/keycontainer`编译器选项[/KEYFILE （指定密钥或密钥对以便为程序集签名）](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly)或[/KEYCONTAINER （指定密钥容器以便为程序集签名）](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly)中的链接器选项C++)。

- 对于.NET Framework v1.0 或 v1.1 中，使用两种<xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>或<xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>属性。

### <a name="sign-your-assembly-with-a-strong-name-in-visual-studio"></a>使用 Visual Studio 中的强名称对程序集签名

1. 在 Visual Studio 中，打开你的解决方案。

2. 在中**解决方案资源管理器**，右键单击项目，然后单击**属性。**

3. 单击**签名**选项卡，然后选择**程序集签名**复选框。

4. 从**选择强名称密钥文件**，选择**新建**。

   **创建强名称密钥**窗口将显示。

5. 在中**密钥文件名称**，键入强名称密钥的名称。

6. 选择是否要使用密码保护密钥，然后单击**确定**。

7. 在中**解决方案资源管理器**，右键单击项目，然后单击**生成**。

### <a name="sign-your-assembly-with-a-strong-name-outside-visual-studio"></a>使用 Visual Studio 外部强名称对程序集签名

使用[强名称工具 (Sn.exe)](/dotnet/framework/tools/sn-exe-strong-name-tool)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果在环境中使用该程序集，则仅禁止显示此规则的警告的篡改内容并不是问题。

## <a name="see-also"></a>请参阅

- <xref:System.Reflection.AssemblyKeyFileAttribute?displayProperty=fullName>
- <xref:System.Reflection.AssemblyKeyNameAttribute?displayProperty=fullName>
- [如何：使用强名称为程序集签名](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [Sn.exe（强名称工具）](/dotnet/framework/tools/sn-exe-strong-name-tool)