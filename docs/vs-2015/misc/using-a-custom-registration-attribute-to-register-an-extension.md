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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935779"
---
# <a name="using-a-custom-registration-attribute-to-register-an-extension"></a>使用自定义注册特性注册扩展
在某些情况下可能需要创建新的注册属性为扩展插件。 若要添加新的注册表项或将新值添加到现有的密钥，可以使用注册属性。 新的属性必须派生自<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>，并且必须重写<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Register%2A>和<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.Unregister%2A>方法。  
  
## <a name="creating-a-custom-attribute"></a>创建自定义属性  
 下面的代码演示如何创建新的注册属性。  
  
```  
[AttributeUsage(AttributeTargets.Class, Inherited = true, AllowMultiple = false)]  
    public class CustomRegistrationAttribute : RegistrationAttribute  
    {  
    }  
  
```  
  
 <xref:System.AttributeUsageAttribute>属性类中用于指定该属性相关，是否可以在一次以上，和是否可以继承的程序元素 （类、 方法等）。  
  
### <a name="creating-a-registry-key"></a>创建注册表项  
 在下面的代码中，创建自定义特性**自定义**子项下为其注册的 VSPackage 的键。  
  
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
  
### <a name="creating-a-new-value-under-an-existing-registry-key"></a>创建现有的注册表项下的新值  
 可以将自定义值添加到现有密钥。 下面的代码演示如何将新值添加到 VSPackage 注册密钥。  
  
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