---
title: 使用自定义注册特性注册扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 98068fa7-bda1-4922-b3f6-28680de58c3d
caps.latest.revision: 3
manager: jillfra
ms.openlocfilehash: a619c5d418df3b9b85ab09cf9b907617ebd81b67
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62935779"
---
# <a name="using-a-custom-registration-attribute-to-register-an-extension"></a>使用自定义注册特性注册扩展
在某些情况下，可能需要为扩展创建新的注册属性。 您可以使用注册属性来添加新的注册表项，或向现有的键添加新的值。 新特性必须派生自 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> ，并且它必须重写 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A> 和 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A> 方法。  
  
## <a name="creating-a-custom-attribute"></a>创建自定义属性  
 下面的代码演示如何创建新的注册属性。  
  
```  
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]  
    public class CustomRegistrationAttribute : RegistrationAttribute  
    {  
    }  
  
```  
  
 <xref:System.AttributeUsageAttribute>用于特性类的指定程序元素 (类、方法等 ) 到特性所属的，是否可以多次使用该元素，以及是否可继承。  
  
### <a name="creating-a-registry-key"></a>创建注册表项  
 在下面的代码中，自定义属性在要注册的 VSPackage 的注册表项下创建一个 **自定义** 子项。  
  
```  
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
  
### <a name="creating-a-new-value-under-an-existing-registry-key"></a>在现有注册表项下创建新值  
 您可以向现有的键添加自定义值。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。  
  
```  
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