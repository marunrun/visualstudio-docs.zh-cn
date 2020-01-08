---
title: 使用 tasks.vs.json launch.vs.json 自定义生成调试任务
ms.date: 02/21/2018
ms.topic: conceptual
helpviewer_keywords:
- NMAKE [Visual Studio]
- makefiles [Visual Studio]
- customize codebases [Visual Studio]
- tasks.vs.json file [Visual Studio]
- launch.vs.json file [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d10b02908c63d177149f9113c37f71813ee09dc
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75567432"
---
# <a name="customize-build-and-debug-tasks-for-open-folder-development"></a>自定义“打开文件夹”开发的生成和调试任务

Visual Studio 清楚如何运行多种语言和代码库，但它并不清楚如何运行所有语言和代码库。 如果在 Visual Studio 中[打开一个代码文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)，且 Visual Studio 知道如何运行代码，便可以立即运行它，而无需任何其他配置。

如果代码库使用 Visual Studio 无法识别的自定义生成工具，你需要提供一些配置详细信息来运行和调试 Visual Studio 中的代码。 指示 Visual Studio 如何通过定义生成任务  来生成代码。 可以通过创建一个或多个生成任务来指定语言生成和运行此代码所需的所有项。 还可以通过创建任意任务来执行你所需的几乎所有操作。 例如，可以创建一个任务来列出文件夹的内容或者重命名文件。

使用以下 .json  文件来自定义无项目代码库：

|文件名|目标|
|-|-|
|tasks.vs.json |指定自定义生成命令和编译器开关，以及任意（与非生成相关）任务。<br>通过“解决方案资源管理器”  右键单击菜单项“配置任务”  进行访问。|
|*launch.vs.json*|指定用于调试的命令行参数。<br>通过“解决方案资源管理器”  右键单击菜单项“调试和启动设置”  进行访问。|

这些 .json  文件位于代码库根文件夹中一个名为 .vs  的隐藏文件夹中。 当你在“解决方案资源管理器”  中的文件或文件夹上选择“配置任务”  或“调试和启动设置”  时，Visual Studio 会根据需要创建 tasks.vs.json  和 launch.vs.json  文件。 这些 json  文件通常处于隐藏状态，因为一般情况下用户不希望在源控件中打开这些文件。 但是如果要在源控件中打开这些文件，请将其拖入代码库的根目录，将在此处显示这些文件。

> [!TIP]
> 若要在 Visual Studio 中查看隐藏文件夹，请在“解决方案资源管理器”工具栏上选择“显示所有文件”按钮   。

## <a name="define-tasks-with-tasksvsjson"></a>使用 tasks.vs.json 定义任务

可以通过直接在 IDE 中作为任务运行来自动执行生成脚本，或者对当前工作区中的现有文件自动执行任何其他外部操作。 可以通过右键单击文件或文件夹并选择“配置任务”  来配置新任务。

![“配置任务”菜单](../ide/media/customize-configure-tasks-menu.png)

这将创建（或打开）.vs  文件夹中的 tasks.vs.json  文件。 可以在此文件中定义生成任务或任意任务，再使用通过“解决方案资源管理器”  右键单击菜单命名的名称来调用它。

可以将自定义任务添加到单个文件，也可以将其添加到某个特定类型的所有文件。 例如，可以将 NuGet 包文件配置为具有“还原包”任务，也可以将所有源文件配置为具有静态分析任务，例如所有 .js  文件的 linter。

### <a name="define-custom-build-tasks"></a>定义自定义生成任务

如果代码库使用 Visual Studio 无法识别的自定义生成工具，则在完成一些配置步骤前，将无法在 Visual Studio 中运行和调试代码。 Visual Studio 提供生成任务  ，你可以在其中了解 Visual Studio 如何生成、重新生成和清除代码。 tasks.vs.json  生成任务文件将 Visual Studio 内部开发循环与代码库所使用的自定义生成工具紧密结合起来。

请考虑一个由名为 hello.cs  的单个 C# 文件构成的代码库。 此类代码库的生成文件可能如下所示  ：

<!-- markdownlint-disable MD010 -->
```makefile
build: directory hello.exe

hello.exe: hello.cs
    csc -debug hello.cs /out:bin\hello.exe

clean:
    del bin\hello.exe bin\hello.pdb

rebuild: clean build

directory: bin

bin:
    md bin
```
<!-- markdownlint-enable MD010 -->

对于此类包含生成、清除和重新生成目标的生成文件，可以定义以下 tasks.vs.json 文件   。 它包含三个用于生成、重新生成和清除代码库的生成任务，使用 NMAKE 作为生成工具。

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "makefile-build",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "build",
      "command": "nmake",
      "args": [ "build" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-clean",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "clean",
      "command": "nmake",
      "args": [ "clean" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-rebuild",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "rebuild",
      "command": "nmake",
      "args": [ "rebuild" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    }
  ]
}
```

当你在 tasks.vs.json  中定义生成任务后，其他右键单击菜单（关联菜单）项会被添加到“解决方案资源管理器”  的相应文件中。 此示例中会将“生成”、“重新生成”和“清除”选项添加至任何生成文件文件的上下文菜单中  。

![带“生成”、“重新生成”和“清除”命令的生成文件上下文菜单](media/customize-build-rebuild-clean.png)

> [!NOTE]
> 由于 `contextType` 设置，这些命令将出现在“配置任务”  命令下的上下文菜单中。 “生成”、“重新生成”和“清除”为生成命令，因此它们会在上下文菜单中间的生成部分中显示。

当你选择其中一个选项，任务将执行。 输出将显示在“输出”  窗口中，而生成错误将显示在“错误列表”  中。

### <a name="define-arbitrary-tasks"></a>定义任意任务

你可以在 tasks.vs.json  文件中定义任意任务，以执行所需的任何操作。 例如，你可以定义一个任务，在“输出”  窗口中显示当前选中的文件的名称，或者在指定目录中列出文件。

以下示例显示定义单个任务的 tasks.vs.json  文件。 调用时，任务会显示当前选中的 .js  文件的文件名。

```json
{
  "version": "0.2.1",
  "tasks": [
    {
      "taskName": "Echo filename",
      "appliesTo": "*.js",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "echo ${file}" ]
    }
  ]
}
```

- `taskName` 指定右键单击菜单中显示的名称。
- `appliesTo` 指定可在其中执行命令的文件。
- `command` 属性指定要调用的命令。 在此示例中，`COMSPEC` 环境变量用于识别命令行解释器，尤其是 cmd.exe  。
- `args` 属性指定要传递到调用命令的参数。
- `${file}` 宏检索“解决方案资源管理器”  中选定的文件。

在保存 tasks.vs.json  后，可以右键单击文件夹中的任何 *.js* 文件并选择“Echo 文件名”  。 文件名将显示在“输出”  窗口中。

> [!NOTE]
> 如果代码库不包含 tasks.vs.json  文件，可通过右键单击或从“解决方案资源管理器”  中文件的上下文菜单选择“配置任务”  ，来创建该文件。

下一个示例定义一个列出 bin  目录文件和子文件夹的任务。

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "List Outputs",
      "appliesTo": "*",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "dir ${outDir}" ]
    }
  ]
}
```

- `${outDir}` 是一个自定义宏，它首先在 `tasks` 块之前定义。 然后在 `args` 属性中对其进行调用。

该任务适用于所有文件。 当你在“解决方案资源管理器”  中打开任何文件的上下文菜单，菜单底部将显示任务名称“列表输出”  。 当你选择“列表输出”  ，“bin”  目录的内容将在 Visual Studio 的“输出”  窗口中列出。

![上下文菜单中的任意任务](../ide/media/customize-arbitrary-task-menu.png)

### <a name="settings-scope"></a>设置范围

代码库的根目录和子目录中可能存在多个 tasks.vs.json  文件。 该设置使代码库中的不同子目录可以灵活具备不同行为。 Visual Studio 在代码库中聚集或覆盖设置，按照以下顺序排列文件：

- 根文件夹 .vs  目录中的设置文件。
- 正在该目录中计算设置。
- 当前目录的父目录，一直到根目录。
- 根目录中的设置文件。

这些聚合规则适用于 tasks.vs.json。  有关如何聚合其他文件中的设置的信息，请参阅本文中该文件的相应部分。

### <a name="properties-for-tasksvsjson"></a>tasks.vs.json 属性

该部分介绍可在 tasks.vs.json  中指定的某些属性。

#### <a name="appliesto"></a>appliesTo

可通过在 `appliesTo` 字段中指定其名称来创建任何文件或文件夹任务，例如 `"appliesTo": "hello.js"`。 以下文件掩码可用作值：

|||
|-|-|
|`"*"`| 任务适用于工作区中的所有文件和文件夹|
|`"*/"`| 任务适用于工作区中的所有文件夹|
|`"*.js"`| 任务适用于工作区中带 .js 扩展名的所有文件 |
|`"/*.js"`| 任务适用于工作区根目录中带 .js 扩展名的所有文件 |
|`"src/*/"`| 任务适用于 src 文件夹的所有子文件夹 |
|`"makefile"`| 任务适用于工作区中的所有生成文件文件 |
|`"/makefile"`| 任务仅适用于工作区根目录中的生成文件 |

#### <a name="macros-for-tasksvsjson"></a>tasks.vs.json 宏

|||
|-|-|
|`${env.<VARIABLE>}`| 指定为开发人员命令提示符设置的任何环境变量（例如，${env.PATH}、${env.COMSPEC} 等）。 有关详细信息，请参阅 [Visual Studio 开发人员命令提示符](/dotnet/framework/tools/developer-command-prompt-for-vs)。|
|`${workspaceRoot}`| 工作区文件夹的完整路径（例如，C:\sources\hello  ）|
|`${file}`| 为再次运行该任务而选择的文件或文件夹的完整路径（例如，C:\sources\hello\src\hello.js  ）|
|`${relativeFile}`| 文件或文件夹的相对路径（例如，src\hello.js  ）|
|`${fileBasename}`| 没有路径或扩展名的文件的名称（例如，hello  ）|
|`${fileDirname}`| 文件的完整路径，不包括文件名（例如，C:\sources\hello\src  ）|
|`${fileExtname}`| 所选文件的扩展名（例如，.js  ）|

## <a name="configure-debugging-with-launchvsjson"></a>使用 launch.vs.json 配置调试

1. 要配置用于调试的代码库，请在“解决方案资源管理器”  中，通过右键单击或从可执行文件的上下文菜单选择“调试和启动设置”  菜单项。

   ![“调试和启动设置”上下文菜单](media/customize-debug-launch-menu.png)

1. 在“选择调试程序”  对话框中，选择一个选项，然后选择“选择”  按钮。

   ![“选择调试程序”对话框](media/customize-select-a-debugger.png)

   如果不存在 launch.vs.json  文件，则创建一个。

   ```json
   {
     "version": "0.2.1",
     "defaults": {},
     "configurations": [
       {
         "type": "default",
         "project": "bin\\hello.exe",
         "name": "hello.exe"
       }
     ]
   }
   ```

1. 接下来，在“解决方案资源管理器”  中右键单击可执行文件，并选择“设为启动项”  。

   可执行文件被指定为代码库的启动项，调试“开始”  按钮的标题将变更，以反映可执行文件的名称。

   ![自定义的“开始”按钮](media/customize-start-button.png)

   按 F5  时，调试程序会在可能已设置的任何断点启动和停止。 所有熟悉的调试程序窗口都是可用的，且具备功能性。

   > [!IMPORTANT]
   > 有关 C++ 打开文件夹项目中自定义生成和调试任务的其他详细信息，请参阅 [Visual Studio 中 C++ 生成系统的打开文件夹支持](/cpp/build/open-folder-projects-cpp)。

### <a name="specify-arguments-for-debugging"></a>指定调试参数

可指定要传入的命令行参数，以便在 launch.vs.json  文件中进行调试。 在 `args` 数组中添加参数，如以下示例所示：

```json
{
  "version": "0.2.1",
  "defaults": {},
  "configurations": [
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe"
    },
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe a1",
      "args": [ "a1" ]
    }
  ]
}
```

保存该文件时，新配置名称将出现在调试目标下拉列表中，你可以选择该名称来启动调试程序。 可以根据需要创建任意数量的调试配置。

![调试配置下拉列表](media/customize-debug-configurations.png)

> [!NOTE]
> 可从以下两个文件位置读取 launch.vs.json  中的 `configurations` 数组属性&mdash;：代码库的根目录和 .vs  目录。 如果存在冲突，则优先考虑 .vs\launch.vs.json  中的值。

## <a name="additional-settings-files"></a>其他设置文件

除了本主题中介绍的三个 .json  文件，Visual Studio 还会从一些其他文件中读取设置，前提是代码库中存在这些文件。

### <a name="vscodesettingsjson"></a>.vscode\settings.json

Visual Studio 从名为 settings.json  的文件中读取限制设置，前提是该文件位于名为 .vscode  的目录中。 此功能用于先前已在 Visual Studio Code 中开发的代码库。 当前，只有从 .vscode\settings.json  读取的设置为 `files.exclude`，该设置在“解决方案资源管理器”中目视筛选文件，或通过一些搜索工具进行筛选。

在代码库中，你可以有任意数量的 .vscode\settings.json  文件。 从文件中读取的设置适用于 .vscode  的父目录及其所有子目录。

### <a name="gitignore"></a>.gitignore

.gitignore  文件用于指示 Git 要忽略的文件，即你不想要查看的文件和目录。 .gitignore  文件通常是代码库的一部分，以便设置可与代码库的所有开发人员共享。 Visual Studio 读取 .gitignore  文件中的模式，以目视筛选项目或者通过一些搜索工具进行筛选。

从 .gitignore  文件中读取的设置适用于该文件的父目录和所有子目录。

## <a name="see-also"></a>请参阅

- [开发代码而无需创建项目或解决方案](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [C++ 的打开文件夹项目](/cpp/build/open-folder-projects-cpp)
- [C++ 的 CMake 项目](/cpp/build/cmake-projects-in-visual-studio)
- [NMAKE 参考](/cpp/build/reference/nmake-reference)
- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
