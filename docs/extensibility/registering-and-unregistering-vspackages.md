---
title: 注册和注销 Vspackage |Microsoft Docs
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
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334295"
---
# <a name="register-and-unregister-vspackages"></a>注册和注销 Vspackage
特性用于注册 VSPackage，但

## <a name="register-a-vspackage"></a>注册 VSPackage
 属性可用于控制托管的 Vspackage 的注册。 中包含的所有注册信息 *.pkgdef*文件。 基于文件的注册的详细信息，请参阅[CreatePkgDef 实用工具](../extensibility/internals/createpkgdef-utility.md)。

 下面的代码演示如何使用标准注册特性注册你的 VSPackage。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[Guid("0B81D86C-0A85-4f30-9B26-DD2616447F95")]
public sealed class BasicPackage : Package
{
    // ...
}
```

## <a name="unregister-an-extension"></a>注销扩展
 如果你已尝试过很多不同的 Vspackage 使用，并想要从实验实例中删除它们，可以只需运行**重置**命令。 寻找**重置 Visual Studio 实验实例**在主页上的计算机，或从命令行运行以下命令：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe" /Reset /VSInstance=14.0 /RootSuffix=Exp
```

 如果你想要卸载已在您的 Visual Studio 的开发实例安装的扩展，请转到**工具** > **扩展和更新**，查找扩展，然后单击**卸载**。

 如果出于某种原因这两个方法成功如何卸载该扩展，则可按如下所示注销 VSPackage 程序集从命令行：

```cmd
<location of Visual Studio 2015 install>\"Microsoft Visual Studio 14.0\VSSDK\VisualStudioIntegration\Tools\Bin\regpkg" /unregister <pathToVSPackage assembly>
```

<a name="using-a-custom-registration-attribute-to-register-an-extension"></a>

## <a name="use-a-custom-registration-attribute-to-register-an-extension"></a>使用自定义注册特性注册扩展

在某些情况下可能需要创建新的注册属性为扩展插件。 若要添加新的注册表项或将新值添加到现有的密钥，可以使用注册属性。 新的属性必须派生自<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>，并且必须重写<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A>和<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A>方法。

### <a name="create-a-custom-attribute"></a>创建自定义属性

下面的代码演示如何创建新的注册属性。

```csharp
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]
public class CustomRegistrationAttribute : RegistrationAttribute
{
}
```

 <xref:System.AttributeUsageAttribute>属性类中用于指定该属性相关，是否可以在一次以上，和是否可以继承的程序元素 （类、 方法等）。

### <a name="create-a-registry-key"></a>创建注册表项

在下面的代码中，创建自定义特性**自定义**子项下为其注册的 VSPackage 的键。

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

### <a name="create-a-new-value-under-an-existing-registry-key"></a>创建现有的注册表项下的新值

可以将自定义值添加到现有密钥。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。

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

## <a name="see-also"></a>请参阅
- [VSPackage](../extensibility/internals/vspackages.md)
