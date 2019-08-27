---
title: RegisterAssembly 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#RegisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, RegisterAssembly task
- RegisterAssembly task [MSBuild]
ms.assetid: ba5f19ac-6764-4d28-9b79-a86de58f8987
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 488ae44a89c203b70e6c8e635d99eb699349156e
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66747326"
---
# <a name="registerassembly-task"></a>RegisterAssembly 任务
读取指定程序集中的元数据，并将所需项添加到注册表中，使 COM 客户端可以透明方式创建 .NET Framework 类。 此任务的行为与 [Regasm.exe（程序集注册工具）](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)的行为类似，但不完全相同。

## <a name="parameters"></a>参数
 下表描述了 `RegisterAssembly` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Assemblies`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要向 COM 注册的程序集。|
|`AssemblyListFile`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 包含 `RegisterAssembly` 任务和 [UnregisterAssembly](../msbuild/unregisterassembly-task.md) 任务之间的状态信息。 此信息可以防止 `UnregisterAssembly` 任务尝试注销无法在 `RegisterAssembly` 任务中注册的程序集。|
|`CreateCodeBase`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则在注册表中创建一个代码库项，它会指定全局程序集缓存中未安装的程序集的文件路径。 如果随后将安装要注册到全局程序集缓存中的程序集，则不应指定此选项。|
|`TypeLibFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定要从指定的程序集中生成的类型库。 生成的类型库包含此程序集中定义的可访问类型的定义。 仅在下列情况之一成立时才会生成此类型库：<br /><br /> -   该位置不存在具有此名称的类型库。<br />-   存在类型库，但其早于要传入的程序集。<br /><br /> 如果类型库比要传递的程序集新，则不会创建新的类型库，但仍会注册程序集。<br /><br /> 如果指定此参数，则其项的数量必须与 `Assemblies` 参数中项的数量相同；否则任务将失败。 如果未指定输入，任务会默认使用程序集的名称，并将项的扩展名更改为 .tlb  。|

## <a name="remarks"></a>备注
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例
 下例使用 `RegisterAssembly` 任务注册由 `MyAssemblies` 项集合指定的程序集。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MyAssemblies Include="MyAssembly.dll" />
    <ItemGroup>

    <Target Name="RegisterAssemblies">
        <RegisterAssembly
            Assemblies="@(MyAssemblies)" >
    </Target>

</Project>
```

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)