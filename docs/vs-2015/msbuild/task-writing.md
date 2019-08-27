---
title: 任务写入 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing tasks
- tasks, creating for MSBuild
- MSBuild, creating tasks
ms.assetid: 3ebc5f87-8f00-46fc-82a1-228f35a6823b
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eaf927b1049709a04d8a883615d1997e9316599e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445385"
---
# <a name="task-writing"></a>任务写入
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

任务提供在生成过程中运行的代码。 任务包含在目标中。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 附带一个典型任务库，也可以创建自己的任务。 有关 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 附带的任务库的详细信息，请参阅[任务参考](../msbuild/msbuild-task-reference.md)。  
  
## <a name="tasks"></a>任务  
 任务的示例包括用于复制一个或多个文件的 [Copy](../msbuild/copy-task.md)、用于创建目录的 [MakeDir](../msbuild/makedir-task.md) 以及用于编译 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 源代码文件的 [Csc](../msbuild/csc-task.md)。 每个任务作为 .NET 类实现，此类实现 Microsoft.Build.Framework.dll 程序集中定义的 <xref:Microsoft.Build.Framework.ITask> 接口。  
  
 实现任务时，有两种方法可供选择：  
  
- 直接实现 <xref:Microsoft.Build.Framework.ITask> 接口。  
  
- 从 Microsoft.Build.Utilities.dll 程序集中定义的帮助程序类 <xref:Microsoft.Build.Utilities.Task> 中派生类。 任务实现 ITask，并提供了一些 ITask 成员的默认实现。 此外，日志记录更为简单。  
  
  在这两种情况下，都必须向类添加一个名为 `Execute` 的方法，也就是在任务运行时调用的方法。 该方法不带任何参数并返回一个 `Boolean` 值：如果任务成功，则返回 `true`；如果失败，则返回 `false`。 以下示例显示一个不执行任何操作并返回 `true` 的任务。  
  
```  
using System;  
using Microsoft.Build.Framework;  
using Microsoft.Build.Utilities;  
  
namespace MyTasks  
{  
    public class SimpleTask : Task  
    {  
        public override bool Execute()  
        {  
            return true;  
        }  
    }  
}  
```  
  
 以下项目文件运行此任务：  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="MyTarget">  
        <SimpleTask />  
    </Target>  
</Project>  
```  
  
 如果在任务类上创建了 .NET 属性，则在运行任务时，它们也可以从项目文件接收输入。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 设置这些属性，并随后立即调用任务的 `Execute` 方法。 要创建字符串属性，请使用任务代码，例如：  
  
```  
using System;  
using Microsoft.Build.Framework;  
using Microsoft.Build.Utilities;  
  
namespace MyTasks  
{  
    public class SimpleTask : Task  
    {  
        public override bool Execute()  
        {  
            return true;  
         }  
  
        private string myProperty;  
        public string MyProperty  
        {  
            get { return myProperty; }  
            set { myProperty = value; }  
        }  
    }  
}  
```  
  
 以下项目文件运行此任务并将 `MyProperty` 设置为给定值：  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <SimpleTask MyProperty="Value for MyProperty" />  
   </Target>  
</Project>  
```  
  
## <a name="registering-tasks"></a>注册任务  
 如果项目将要运行任务，[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 必须知道如何找到包含任务类的程序集。 任务是使用 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md) 注册的。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 文件 Microsoft.Common.Tasks 是一个包含 `UsingTask` 元素列表的项目文件，这些元素注册随 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 一起提供的所有任务。 生成每个项目时会自动包括该文件。 如果在 Microsoft.Common.Tasks 中注册的任务也在当前项目文件中进行了注册，则当前项目文件具有优先权；也就是说，可以使用自己的同名任务重写默认任务。  
  
> [!TIP]
> 通过查看 Microsoft.Common.Tasks 的内容，可以看到随 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 一起提供的任务列表。  
  
## <a name="raising-events-from-a-task"></a>从任务引发事件  
 如果任务派生自 <xref:Microsoft.Build.Utilities.Task> 帮助器类，可以使用 <xref:Microsoft.Build.Utilities.Task> 类上的下列任一帮助器方法来引发由任何注册的记录器捕获并显示的事件：  
  
```  
public override bool Execute()  
{  
    Log.LogError("messageResource1", "1", "2", "3");  
    Log.LogWarning("messageResource2");  
    Log.LogMessage(MessageImportance.High, "messageResource3");  
    ...  
}  
```  
  
 如果任务直接实现 <xref:Microsoft.Build.Framework.ITask>，仍可以引发此类事件，但必须使用 IBuildEngine 接口。 以下示例显示一个实现 ITask 并引发自定义事件的任务：  
  
```  
public class SimpleTask : ITask  
{  
    private IBuildEngine buildEngine;  
    public IBuildEngine BuildEngine  
    {  
        get{ return buildEngine; }  
        set{ buildEngine = value; }  
    }  
  
    public override bool Execute()  
    {  
        TaskEventArgs taskEvent =  
            new TaskEventArgs(BuildEventCategory.Custom,  
            BuildEventImportance.High, "Important Message",  
           "SimpleTask");  
        BuildEngine.LogBuildEvent(taskEvent);  
        return true;  
    }  
}  
```  
  
## <a name="requiring-task-parameters-to-be-set"></a>要求设置任务参数  
 可以将特定任务属性标记为“必需”，使任何运行该任务的项目文件都必须对这些属性设置值，否则生成将会失败。 将 `[Required]` 特性应用到任务的 .NET 属性，如下所示：  
  
```  
private string requiredProperty;  
  
[Required]  
public string RequiredProperty  
{  
    get { return requiredProperty; }  
    set { requiredProperty = value; }  
}  
```  
  
 `[Required]` 特性由 <xref:Microsoft.Build.Framework> 命名空间中的 <xref:Microsoft.Build.Framework.RequiredAttribute> 定义。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 以下 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 类演示一个从 <xref:Microsoft.Build.Utilities.Task> 帮助器类派生的任务。 该任务返回 `true`，表示执行成功。  
  
### <a name="code"></a>代码  
  
```  
using System;  
using Microsoft.Build.Utilities;  
  
namespace SimpleTask1  
{  
    public class SimpleTask1: Task  
    {  
        public override bool Execute()  
        {  
            // This is where the task would presumably do its work.  
            return true;  
        }  
    }  
}  
```  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 以下 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 类演示一个实现 <xref:Microsoft.Build.Framework.ITask> 接口的任务。 该任务返回 `true`，表示执行成功。  
  
### <a name="code"></a>代码  
  
```  
using System;  
using Microsoft.Build.Framework;  
  
namespace SimpleTask2  
{  
    public class SimpleTask2: ITask  
    {  
        //When implementing the ITask interface, it is necessary to  
        //implement a BuildEngine property of type  
        //Microsoft.Build.Framework.IBuildEngine. This is done for  
        //you if you derive from the Task class.  
        private IBuildEngine buildEngine;  
        public IBuildEngine BuildEngine  
        {  
            get  
            {  
                return buildEngine;  
            }  
            set  
            {  
                buildEngine = value;  
            }  
         }  
  
        // When implementing the ITask interface, it is necessary to  
        // implement a HostObject property of type Object.  
        // This is done for you if you derive from the Task class.  
        private Object hostObject;  
        public Object HostObject  
        {  
            get  
            {  
                return hostObject;  
            }  
  
            set  
            {  
                hostObject = value;  
            }  
        }  
  
        public bool Execute()  
        {  
            // This is where the task would presumably do its work.  
            return true;  
        }  
    }  
}  
```  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 此 [!INCLUDE[csprcs](../includes/csprcs-md.md)] 类演示一个从 <xref:Microsoft.Build.Utilities.Task> 帮助器类派生的任务。 它有一个必需的字符串属性，并引发一个由所有注册的记录器显示的事件。  
  
### <a name="code"></a>代码  
 [!code-csharp[msbuild_SimpleTask3#1](../snippets/csharp/VS_Snippets_Misc/msbuild_SimpleTask3/CS/SimpleTask3.cs#1)]  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 以下示例显示一个调用上一示例任务 SimpleTask3 的项目文件。  
  
### <a name="code"></a>代码  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <UsingTask TaskName="SimpleTask3.SimpleTask3"   
        AssemblyFile="SimpleTask3\bin\debug\simpletask3.dll"/>  
  
    <Target Name="MyTarget">  
        <SimpleTask3 MyProperty="Hello!"/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
