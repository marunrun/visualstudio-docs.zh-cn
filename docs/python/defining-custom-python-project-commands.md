---
title: 为 Python 项目定义自定义菜单命令
description: 通过编辑项目和目标文件，可以将自定义命令添加到 Visual Studio 中的 Python 项目上下文菜单，用于调用可执行程序、脚本、模块、内联代码片段和 pip。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: ec53a67980866ed6422fae5764bbf6a9313ef91e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62957644"
---
# <a name="define-custom-commands-for-python-projects"></a>为 Python 项目定义自定义命令

在处理 Python 项目的过程中，可观察到系统切换到命令窗口来运行特定脚本或模块、运行 pip 命令或运行一些其他任意工具。 为改进工作流，可将自定义命令添加到 Python 项目上下文菜单的 Python 子菜单中。 可在控制台窗口或 Visual Studio“输出”窗口中运行这些命令。 还可使用正则表达式来指示 Visual Studio 如何分析来自命令输出的错误和警报。

默认情况下，此菜单仅包含单个 Run PyLint 命令：

![项目上下文菜单上 Python 子菜单的默认外观](media/custom-commands-default-menu.png)

自定义命令也显示在此上下文菜单中。 直接向项目文件添加自定义命令，这些命令在此处应用到上述单个项目中。 还可在 .targets 文件中定义自定义命令，这些命令可轻松导入多个项目文件。

Visual Studio 中的某些 Python 项目模板已使用其 .targets 文件添加其自身的自定义命令。 例如，Bottle Web 项目和 Flask Web 项目模板均添加“启动服务器”和“启动调试服务器”这两个命令。 Django Web 项目模板也会添加这些命令，但还会再添加一些项：

![Django 项目上下文菜单上 Python 子菜单的外观](media/custom-commands-django-menu.png)

每个自定义命令都可引用 Python 文件、Python 模块、内联 Python 代码、任意可执行文件或 pip 命令。 还可指定命令运行的方式和位置。

> [!Tip]
> 每次在文本编辑器中更改项目文件时，都必须在 Visual Studio 中重新加载项目才能应用这些更改。 例如，必须先重新加载项目，才能向要在项目上下文菜单上显示的这些命令添加自定义命令。
>
> 如你所知，Visual Studio 提供直接编辑项目文件的方式。 首先右键单击项目文件并选择“卸载项目”，然后再次右键单击并选择“编辑 \<项目名称>”，才能在 Visual Studio 编辑器中打开项目。 然后，编辑内容并进行保存，再次右键单击项目，再选择“重新加载项目”，此时系统也会提示你确认关闭编辑器中的项目文件。
>
> 但在开发自定义命令时，所有这些单击都变得繁琐。 要提升工作流效率，请在 Visual Studio 中加载项目，并同时在单独的编辑器中一并打开 .pyproj 文件（例如 Visual Studio、Visual Studio Code 和记事本等的其他实例）。 保存在编辑器中所做的更爱并切换到 Visual Studio 时，Visual Studio 会检测所做更改，并询问是否要重新加载项目（已在环境外部修改项目 \<名称>）。 选择“重新加载”，只需一步即可应用所做更改。

## <a name="walkthrough-add-a-command-to-a-project-file"></a>演练：向项目文件添加命令

此部分将演示一个使用 python.exe 直接运行项目启动文件的简单示例，有助于熟悉自定义命令。 （此类命令的作用等同于使用“调试” > “启动但不调试”。）

1. 使用“Python 应用程序”模板新建一个名为“Python-CustomCommands”的项目。 （如果尚不熟悉流程，请参阅[快速入门：基于模板创建 Python 项目](quickstart-02-python-in-visual-studio-project-from-template.md)以获取相关说明。）

1. 在 Python_CustomCommands.py 中，添加代码 `print("Hello custom commands")`。

1. 在“解决方案资源管理器”中右键单击项目，再选择“Python”。请注意，子菜单中仅显示 Run PyLint 命令。 自定义命令也显示在此子菜单上。

1. 根据说明中建议的操作，在单独的文本编辑器中打开 Python-CustomCommands.pyproj。 然后，在恰好位于结尾的 `</Project>` 内的文件末尾添加以下行，然后保存文件。

    ```xml
    <PropertyGroup>
      <PythonCommands>
        $(PythonCommands);
      </PythonCommands>
    </PropertyGroup>
    ```

1. 切换回到 Visual Studio，并在系统提示出现文件更改时选择“重新加载”。 然后再次检查“Python”菜单，查看 Run PyLint 是否仍是此处显示的唯一项，因为所添加的行仅复制包含 PyLint 命令的默认 `<PythonCommands>` 属性组。

1. 通过项目文件切换到编辑器，并在 `<PropertyGroup>` 的后面添加以下 `<Target>` 定义。 如本文稍后所述，此 `Target` 元素定义一个在控制台窗口使用 python.exe 运行启动文件（由“StartupFile”属性标识）的自定义命令。 此 `ExecuteIn="consolepause"` 属性使用一个在你按键后才关闭的控制台。

    ```xml
    <Target Name="Example_RunStartupFile" Label="Run startup file" Returns="@(Commands)">
      <CreatePythonCommandItem
        TargetType="script"
        Target="$(StartupFile)"
        Arguments=""
        WorkingDirectory="$(MSBuildProjectDirectory)"
        ExecuteIn="consolepause">
        <Output TaskParameter="Command" ItemName="Commands" />
      </CreatePythonCommandItem>
    </Target>
    ```

1. 将目标的 `Name` 属性的值添加到之前添加的 `<PythonCommands>` 属性组，让元素如以下代码所示。 将目标名称添加到此列表就是指将其添加到 Python 菜单。

    ```xml
      <PythonCommands>
        $(PythonCommands);
        Example_RunStartupFile
      </PythonCommands>
    ```

    如果希望命令显示在 `$(PythonCommands)` 中定义的项之前，请将其放在此标记的前面。

1. 保存项目文件，切换到 Visual Studio，然后在系统提示时重新加载项目。 右键单击“Python-CustomCommands”项目并选择“Python”。 菜单上应该会显示“运行启动文件”项。 如果未显示菜单项，请检查是否已将名称添加到 `<PythonCommands>` 元素。 另请参阅本文稍后部分中的[疑难解答](#troubleshooting)。

    ![Python 上下文子菜单上显示的自定义命令](media/custom-commands-walkthrough-menu-item.png)

1. 选择“运行启动文件”命令，此时应会显示一个命令窗口，窗口上显示“了解自定义命令”且后接“按任意键继续操作。  按相关键关闭窗口。

    ![控制台窗口中的自定义命令输出](media/custom-commands-walkthrough-console.png)

1. 通过项目文件返回到编辑器，并将 `ExecuteIn` 属性的值更改为 `output`。 保存文件，切换到 Visual Studio，再重新加载项目，然后再次调用命令。 此时，Visual Studio 的“输出”窗口中会显示项目的输出：

    ![输出窗口中的自定义命令输出](media/custom-commands-walkthrough-output-window.png)

1. 要添加更多命令，请为每个命令定义适当的 `<Target>` 元素，将目标的名称添加到 `<PythonCommands>` 属性组，并在 Visual Studio 中重新加载项目。

>[!Tip]
> 如果调用要使用项目属性的命令（例如 `($StartupFile)`），且此命令由于标记未定义而失败，则在你重新加载项目之前，Visual Studio 会禁用此命令。 但是，更改会定义属性的项目之后，不会刷新这些命令的状态，因此仍需在此类情况下重新加载项目。

## <a name="command-target-structure"></a>命令目标结构

`<Target>` 元素通常按以下伪代码形式显示：

```xml
<Target Name="Name1" Label="Display Name" Returns="@(Commands)">
    <CreatePythonCommandItem Target="filename, module name, or code"
        TargetType="executable/script/module/code/pip"
        Arguments="..."
        ExecuteIn="console/consolepause/output/repl[:Display name]/none"
        WorkingDirectory="..."
        ErrorRegex="..."
        WarningRegex="..."
        RequiredPackages="...;..."
        Environment="...">

      <!-- Output always appears in this form, with these exact attributes -->
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

若要在属性值中引用项目属性或环境变量，请使用 `$()` 标记中的名称，例如 `$(StartupFile)` 和 `$(MSBuildProjectDirectory)`。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

### <a name="target-attributes"></a>Target 属性

| 特性 | 必需 | 说明 |
| --- | --- | --- |
| name | 是 | Visual Studio 项目中命令的标识符。 必须将此名称添加到 `<PythonCommands>` 组，Python 子菜单上才会显示命令。 |
| Label | 是 | Python 子菜单中出现的 UI 显示名称。 |
| 返回 | 是 | 必须包含将目标标识为命令的 `@(Commands)`。 |

### <a name="createpythoncommanditem-attributes"></a>CreatePythonCommandItem 属性

属性值均不区分大小写。

| 特性 | 必需 | 说明 |
| --- | --- | --- |
| TargetType | 是 | 指定 Target 属性包含的内容以及如何将其与 Arguments 属性一并使用：<ul><li>**可执行文件：** 运行在 Target 中命名的可执行文件，附加 Arguments 的值，就如在命令行中直接输入一般。 值仅可包含项目名称且不可带有参数。</li><li>**脚本**：向 Target 中的文件名运行 python.exe，再执行 Arguments 中的值。</li><li>**模块**：在 Target 中运行后接模块名的 `python -m`，再运行 Arguments 中的值。</li><li>**代码**：运行 Target 中包含的内联代码。 这会忽略 Arguments 值。</li><li>**pip**：通过 Target 中的命令运行 `pip`，后接 Arguments；但如果 ExecuteIn 设置为“输出”，pip 则假定 `install` 命令并使用 Target 作为包名称。</li></ul> |
| Target | 是 | 要使用的文件名、模块名、代码或 pip 命令（取决于 TargetType）。 |
| 自变量 | Optional | 指定要赋值给目标的参数字符串（若有）。 请注意，如果 TargetType 是 `script`，则向 Python 项目赋予参数，而不是 python.exe。 `code` TargetType 忽略此项。 |
| ExecuteIn | 是 | 指定要运行命令的环境：<ul><li>**控制台**：（默认）如同直接在命令行上直接输入 Target 和 Arguments 一样运行它们。 这会在运行 Target 时显示命令窗口，该窗口随后自动关闭。</li><li>**consolepause**：与控制台相同，但必须按键才能关闭窗口。</li><li>**输出**：运行 Target 并在 Visual Studio 的“输出”窗口中显示其结果。 如果 TargetType 为“pip”，则 Visual Studio 使用 Target 作为包名称并附加 Arguments。</li><li>**repl**：在 [Python 交互式](python-interactive-repl-in-visual-studio.md)窗口中运行 Target；可选显示名称用作窗口的标题。</li><li>无：与控制台的行为相同。</li></ul>|
| WorkingDirectory | Optional | 要在其中运行命令的文件夹。 |
| ErrorRegex<br>WarningRegEx | Optional | 仅可在 ExecuteIn 为 `output` 时使用。 这两个值均指定一个正则表达式，Visual Studio 使用此表达式来分析命令输出，以在“错误列表”窗口中显示错误和警报。 若未指定，则命令不会影响“错误列表”窗口。 有关 Visual Studio 所需内容的详细信息，请参阅[命令的捕获组](#named-capture-groups-for-regular-expressions)。 |
| RequiredPackages | Optional | 命令的包请求列表，其中命令的格式与 [requirements.txt](https://pip.readthedocs.io/en/1.1/requirements.html) 相同 (pip.readthedocs.io)。 “运行 PyLint”命令，例如指定 `pylint>=1.0.0`。 运行命令之前，Visual Studio 会先检查是否已安装列表中的所有包。 Visual Studio 使用 pip 命令来安装缺少的包。 |
| 环境 | Optional | 运行命令前要定义的环境变量的字符串。 每个变量均使用 \<NAME>=\<VALUE> 形式，多个变量用分号隔开。 具有多个值的变量必须用单引号或双引号引起来，例如 'NAME=VALUE1;VALUE2' 形式。 |

#### <a name="named-capture-groups-for-regular-expressions"></a>正则表达式中已命名的捕获组

在分析来自命令输出的错误和警报时，Visual Studio 期望 `ErrorRegex` 和 `WarningRegex` 值中的正则表达式使用以下命名组：

- `(?<message>...)`：错误文本
- `(?<code>...)`：错误代码
- `(?<filename>...)`：报告其出现错误的文件的名称
- `(?<line>...)`：报告其出现错误的文件的位置行号。
- `(?<column>...)`：报告其出现错误的文件的位置列号。

例如，PyLint 生成以下形式的警报：

```output
************* Module hello
C:  1, 0: Missing module docstring (missing-docstring)
```

“运行 Pylint”命令的 `WarningRegex` 值必须如下所示，Visual Studio 才能从此类警报中提取正确的信息并将其显示在“错误列表”窗口中：

```regex
^(?<filename>.+?)\((?<line>\d+),(?<column>\d+)\): warning (?<msg_id>.+?): (?<message>.+?)$]]
```

（请注意：值中的 `msg_id` 实际上应为 `code`具体请参见[问题 3680](https://github.com/Microsoft/PTVS/issues/3680)。）

## <a name="create-a-targets-file-with-custom-commands"></a>使用自定义命令创建 .targets 文件

如果在项目文件中定义自定义命令，则该命令仅在此项目文件中可用。 要在多个项目文件中使用命令，必须在 .targets 文件中定义 `<PythonCommands>` 属性组以及所具备的所有 `<Target>` 元素。 然后将此文件导入到单个项目文件中。

.targets 文件采用以下格式：

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <PythonCommands>
      $(PythonCommands);
      <!-- Additional command names -->
    </PythonCommands>
  </PropertyGroup>

  <Target Name="..." Label="..." Returns="@(Commands)">
    <!-- CreatePythonCommandItem and Output elements... -->
  </Target>

  <!-- Any number of additional Target elements-->
</Project>
```

要将 .targets 文件加载到项目中，需将 `<Import Project="(path)">` 元素置于 `<Project>` 元素中（位置不限）。 例如，如果项目的 targets 子文件夹中具有名为 CustomCommands.targets 的文件，请使用以下代码：

```xml
<Import Project="targets/CustomCommands.targets"/>
```

> [!Note]
> 每次更改 .targets 文件时，都需要重新加载包含项目的解决方案，而不是加载项目本身。

## <a name="example-commands"></a>示例命令

### <a name="run-pylint-module-target"></a>运行 PyLint（模块目标）

以下代码显示在 Microsoft.PythonTools.targets 文件中：

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);PythonRunPyLintCommand</PythonCommands>
  <PyLintWarningRegex>
    <![CDATA[^(?<filename>.+?)\((?<line>\d+),(?<column>\d+)\): warning (?<msg_id>.+?): (?<message>.+?)$]]>
  </PyLintWarningRegex>
</PropertyGroup>

<Target Name="PythonRunPyLintCommand"
        Label="resource:Microsoft.PythonTools.Common;Microsoft.PythonTools.Common.Strings;RunPyLintLabel"
        Returns="@(Commands)">
  <CreatePythonCommandItem Target="pylint.lint"
                           TargetType="module"
                           Arguments="&quot;--msg-template={abspath}({line},{column}): warning {msg_id}: {msg} [{C}:{symbol}]&quot; -r n @(Compile, ' ')"
                           WorkingDirectory="$(MSBuildProjectDirectory)"
                           ExecuteIn="output"
                           RequiredPackages="pylint&gt;=1.0.0"
                           WarningRegex="$(PyLintWarningRegex)">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-pip-install-with-a-specific-package-pip-target"></a>向特定的包（pip 目标）运行 pip install

以下命令在“输出”窗口运行 `pip install my-package`。 可在开发包和测试其安装项的情况下运行此命令。 请注意，Target 中具有包名称而不是 `install` 命令，使用 `ExecuteIn="output"` 时假定为后者。

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);InstallMyPackage</PythonCommands>
</PropertyGroup>

<Target Name="InstallMyPackage" Label="pip install my-package" Returns="@(Commands)">
  <CreatePythonCommandItem Target="my-package" TargetType="pip" Arguments=""
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="output">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="show-outdated-pip-packages-pip-target"></a>显示过时的 pip 包（pip 目标）

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);ShowOutdatedPackages</PythonCommands>
</PropertyGroup>

<Target Name="ShowOutdatedPackages" Label="Show outdated pip packages" Returns="@(Commands)">
  <CreatePythonCommandItem Target="list" TargetType="pip" Arguments="-o --format columns"
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="consolepause">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-an-executable-with-consolepause"></a>通过 consolepause 运行可执行文件

以下命令只需运行 `where` 即可显示出在项目文件夹中启动 Python 文件：

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);ShowAllPythonFilesInProject</PythonCommands>
</PropertyGroup>

<Target Name="ShowAllPythonFilesInProject" Label="Show Python files in project" Returns="@(Commands)">
  <CreatePythonCommandItem Target="where" TargetType="executable" Arguments="/r . *.py"
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="output">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-server-and-run-debug-server-commands"></a>运行服务器和调试服务器命令

要了解如何为 Web 项目定义“启动服务器”和“启动调试服务器”命令，请查看 [Microsoft.PythonTools.Web.targets](https://github.com/Microsoft/PTVS/blob/master/Python/Product/BuildTasks/Microsoft.PythonTools.Web.targets) (GitHub)。

### <a name="install-package-for-development"></a>安装开发程序包

```xml
<PropertyGroup>
  <PythonCommands>PipInstallDevCommand;$(PythonCommands);</PythonCommands>
</PropertyGroup>

<Target Name="PipInstallDevCommand" Label="Install package for development" Returns="@(Commands)">
    <CreatePythonCommandItem Target="pip" TargetType="module" Arguments="install --editable $(ProjectDir)"
        WorkingDirectory="$(WorkingDirectory)" ExecuteIn="Repl:Install package for development">
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

*来自 [fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub)，经授权使用。*

### <a name="generate-windows-installer"></a>生成 Windows Installer

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);BdistWinInstCommand;</PythonCommands>
</PropertyGroup>

<Target Name="BdistWinInstCommand" Label="Generate Windows Installer" Returns="@(Commands)">
    <CreatePythonCommandItem Target="$(ProjectDir)setup.py" TargetType="script"
        Arguments="bdist_wininst --user-access-control=force --title &quot;$(InstallerTitle)&quot; --dist-dir=&quot;$(DistributionOutputDir)&quot;"
        WorkingDirectory="$(WorkingDirectory)" RequiredPackages="setuptools"
        ExecuteIn="Repl:Generate Windows Installer">
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

*来自 [fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub)，经授权使用。*

### <a name="generate-wheel-package"></a>生成滚轮程序包

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);BdistWheelCommand;</PythonCommands>
</PropertyGroup>

<Target Name="BdistWheelCommand" Label="Generate Wheel Package" Returns="@(Commands)">

  <CreatePythonCommandItem Target="$(ProjectDir)setup.py" TargetType="script"
      Arguments="bdist_wheel --dist-dir=&quot;$(DistributionOutputDir)&quot;"
      WorkingDirectory="$(WorkingDirectory)" RequiredPackages="wheel;setuptools"
      ExecuteIn="Repl:Generate Wheel Package">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

*来自 [fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub)，经授权使用。*

## <a name="troubleshooting"></a>疑难解答

### <a name="message-the-project-file-could-not-be-loaded"></a>消息:“无法加载项目文件”

表示项目文件中存在语法错误。 此消息包含具有行号和字符位置的具体错误。

### <a name="console-window-closes-immediately-after-command-is-run"></a>运行命令后立即关闭控制台窗口

使用 `ExecuteIn="consolepause"` 而非 `ExecuteIn="console"`。

### <a name="command-does-not-appear-on-the-menu"></a>菜单中未显示命令

检查命令是否包含在 `<PythonCommands>` 属性组中，以及命令列表中的名称是否与 `<Target>` 元素中指定的元素相匹配。

例如在下例中，属性组中的“Example”名称与目标中的“ExampleCommand”名称不匹配。 Visual Studio 未找到名为“Example”的命令，因此不显示任何命令。 请在命令列表中使用“ExampleCommand”，或只将目标的名称更改为“Example”。

```xml
  <PropertyGroup>
    <PythonCommands>$(PythonCommands);Example</PythonCommands>
  </PropertyGroup>
  <Target Name="ExampleCommand" Label="Example Command" Returns="@(Commands)">
    <!-- ... -->
  </Target>
```

### <a name="message-an-error-occurred-while-running-command-name-failed-to-get-command-target-name-from-project"></a>消息:“运行 \<命名名称> 时出错。 未能从项目中获取命令 \<目标名称>。”

表示 `<Target>` 或 `<CreatePythonCommandItem>` 元素中的内容不正确。 原因可能为：

- 所需的 `Target` 属性为空。
- 所需的 `TargetType` 属性为空或包含不可识别的值。
- 所需的 `ExecuteIn` 属性为空或包含不可识别的值。
- 指定了 `ErrorRegex` 或 `WarningRegex`，但未指定 `ExecuteIn="output"` 设置。
- 元素中存在不可识别的属性。 例如，可能使用了 `Argumnets`（拼写错误）而不是 `Arguments`。

如果引用未定义的属性，则属性值可能为空。 例如，例如使用 `$(StartupFile)` 标记，但未在项目中定义任何启动文件，则标记解析为空字符串。 此类情况下，可能需要定义一个默认值。 例如，如果尚未在项目属性中指定服务器启动文件，则在 Bottle，Flask 和 Django 项目模板中定义的“Run server”和“Run debug server”命令将默认为 manage.py。

### <a name="visual-studio-hangs-and-crashes-when-running-the-command"></a>运行命令时，Visual Studio 挂起且出现崩溃

你可能在尝试通过 `ExecuteIn="output"` 运行控制台命令，此时 Visual Studio 可能在尝试分析输出时崩溃。 请改用 `ExecuteIn="console"`。 （请参阅[问题 3682](https://github.com/Microsoft/PTVS/issues/3681)。）

### <a name="executable-command-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a>可执行命令“未被识别为内部或外部命令、可操作程序或批处理文件”

使用 `TargetType="executable"` 时，`Target` 中的值只能是不带任何参数的程序名称，例如仅为 python 或仅为 python.exe。 将所有参数移动到 `Arguments` 属性中。
