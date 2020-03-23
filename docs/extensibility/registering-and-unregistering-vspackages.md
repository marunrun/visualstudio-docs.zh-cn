---
title: 注册和取消注册 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, VSPackages
- VSPackages, registering
ms.assetid: e25e7a46-6a55-4726-8def-ca316f553d6b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 701700ba9d5c6db1e5858a2419e1b2c0fa950ae5
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301583"
---
# <a name="register-and-unregister-vspackages"></a>注册和取消注册 VS 包
您可以使用属性注册 VSPackage，但

## <a name="register-a-vspackage"></a>注册 VS 包
 您可以使用属性来控制托管 VSPackages 的注册。 所有注册信息都包含在 *.pkgdef*文件中。 有关基于文件的注册的详细信息，请参阅[CreatePkgDef 实用程序](../extensibility/internals/createpkgdef-utility.md)。

 以下代码演示如何使用标准注册属性来注册 VSPackage。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>注销扩展
 如果您一直在试验许多不同的 VSPackages，并希望从实验实例中删除它们，则可以运行 **"重置"** 命令。 在计算机的起始页上查找**重置可视化工作室实验实例**，或从命令行运行此命令：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 如果要卸载在 Visual Studio 的开发实例上安装的扩展，请转到 **"工具** > **扩展"和"更新**"，查找扩展，然后单击"**卸载**"。

 如果由于某种原因，这些方法都无法成功卸载扩展，则可以从命令行中取消注册 VSPackage 程序集，如下所示：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>使用自定义注册属性注册扩展

在某些情况下，您可能需要为扩展创建新的注册属性。 可以使用注册属性添加新注册表项或向现有键添加新值。 新属性必须派生自<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>，并且必须重写<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A>和 方法<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A>。

### <a name="create-a-custom-attribute"></a>创建自定义属性

以下代码演示如何创建新的注册属性。

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 <xref:System.AttributeUsageAttribute>用于属性类，以指定属性相关的程序元素（类、方法等），是否可以多次使用该元素，以及是否可以继承该元素。

### <a name="create-a-registry-key"></a>创建注册表项

在以下代码中，自定义属性在正在注册的 VSPackage 的密钥下创建**自定义**子键。

```csharp
public override void Register(RegistrationAttribute.RegistrationContext context)
{
    Key packageKey = null;
    try
    {
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + @"}\Custom");
        packageKey.SetValue("NewCustom", 1);
    }
    finally
    {
        if (packageKey != null)
            packageKey.Close();
    }
}

public override void Unregister(RegistrationContext context)
{
    context.RemoveKey(@"Packages\" + context.ComponentType.GUID + @"}\Custom");
}
```

### <a name="create-a-new-value-under-an-existing-registry-key"></a>在现有注册表项下创建新值

您可以将自定义值添加到现有键。 以下代码演示如何向 VSPackage 注册密钥添加新值。

```csharp
public override void Register(RegistrationAttribute.RegistrationContext context)
{
    Key packageKey = null;
    try
    {
        packageKey = context.CreateKey(@"Packages\{" + context.ComponentType.GUID + "}");
        packageKey.SetValue("NewCustom", 1);
    }
    finally
    {
        if (packageKey != null)
            packageKey.Close();
    }
}

public override void Unregister(RegistrationContext context)
{
    context.RemoveValue(@"Packages\" + context.ComponentType.GUID, "NewCustom");
}
```

## <a name="see-also"></a>另请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
