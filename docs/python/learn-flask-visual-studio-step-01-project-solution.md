---
title: 了解 Visual Studio 中的 Flask 教程步骤 1，Flask 基础知识
titleSuffix: ''
description: Visual Studio 项目上下文中的 Flask 基础知识演练，包括先决条件、Git 和虚拟环境。
ms.date: 01/07/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 7707d993ac5fb6f73060d0f862c828e67c833872
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79300881"
---
# <a name="tutorial-get-started-with-the-flask-web-framework-in-visual-studio"></a>教程：在 Visual Studio 中开始使用 Flask Web 框架

[Flask](https://palletsprojects.com/p/flask/) 是一种轻量级 Web 应用程序 Python 框架，为 URL 路由和页面呈现提供基础知识。

Flask 被称为“微”框架，因为它不直接提供窗体验证、数据库抽象、身份验证等功能。 此类功能改为由名为 Flask 扩展的特殊 Python 包提供  。 这些扩展无缝集成 Flask，所以看起来就像 Flask 本身的一部分。 例如，Flask 本身不提供页模板引擎。 Jinja、Jade 等扩展提供模板化，如本教程所示。

在本教程中，你将了解：

> [!div class="checklist"]
> - 使用“空白 Flask Web 项目”模板在 Git 存储库中创建一个基本 Flask 项目（步骤 1）
> - 使用模板创建一个单页 Flask 应用，并呈现该页面（步骤 2）
> - 为静态文件提供服务、添加页面和使用模板继承（步骤 3）
> - 使用 Flask Web 项目模板创建包含多个页面和响应式设计的应用（步骤 4）
> - 使用“投票 Flask Web 项目”模板创建使用多种存储选项（Azure 存储、MongoDB 或内存）的投票应用。

在这些步骤的过程中，将创建一个包含三个单独项目的 Visual Studio 解决方案。 使用 Visual Studio 中包含的不同 Flask 项目模板创建项目。 通过将项目保留在同一解决方案中，可以轻松地在不同文件之间来回切换以进行比较。

> [!Note]
> 本教程与 [Flask 快速入门](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)的区别在于，可以更详细地了解 Flask 并了解如何使用不同的 Flask 项目模板（为自己的项目提供更全面的起点）。 例如，创建项目时，项目模板自动安装 Flask 包，而无需按快速入门所示手动安装包。

## <a name="prerequisites"></a>系统必备

- Windows 版 Visual Studio 2017 及以上版本，且具有以下选项：
  - “Python 开发”工作负载（安装程序中的“工作负载”选项卡）   。 有关说明，请参阅[在 Visual Studio 中安装 Python 支持](installing-python-support-in-visual-studio.md)。
  - “代码工具”下“单个组件”选项卡上的“适用于 Windows 的 Git”和“适用于 Visual Studio 的 GitHub 扩展”     。

针对 Visual Studio 的 Python 工具的所有早期版本都附带 Flask 项目模板，虽然详细信息可能与本教程提供的信息有所出入。

Visual Studio for Mac 当前不支持 Python 开发。 在 Mac 和 Linux 上，使用 [Visual Studio Code 中的 Python 扩展](https://code.visualstudio.com/docs/python/python-tutorial)。

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>步骤 1-1：创建 Visual Studio 项目和解决方案

1. 在 Visual Studio 中，选择“文件” **“新建”** “项目”，搜索“Flask”，然后选择“空白 Flask Web 项目”模板 >    >    。 （还可以在左侧列表的“Python”   > “Web”  中找到模板。）

    ![Visual Studio 中“空白 Flask Web 项目”的新建项目对话框](media/flask/step01-new-blank-project.png)

1. 在对话框底部的字段中，输入以下信息（如上图所示），然后选择“确定”  ：

    - **名称**：将 Visual Studio 项目的名称设置为“BasicProject”  。 此名称还用于 Flask 项目。
    -  位置：指定要在其中创建 Visual Studio 解决方案和项目的位置。
    - **解决方案名称**：设置为“LearningFlask”，适用于本教程中作为多个项目的容器的解决方案  。
    -  为解决方案创建目录：保留设置（默认设置）。
    -  创建新的 Git 存储库：选择此选项（默认情况下会清除该选项），以便在 Visual Studio 创建解决方案时创建本地 Git 存储库。 如果未看到此选项，请运行 Visual Studio 安装程序并在“代码工具”下的“单个组件”选项卡上添加“适用于 Windows 的 Git”和“适用于 Visual Studio 的 GitHub 扩展”     。

1. 稍后 Visual Studio 会显示一个对话框，提示“此项目需要外部包”（如下所示）  。 显示此对话框是因为该模板包含引用最新 Flask 1.x 包的 requirements.txt 文件  。 （选择“显示所需包”  查看确切的依赖项。）

    ![指示项目需要外部包的提示](media/tutorials-common/step01-requirements-prompt-install-myself.png)

1. 选择选项“我将自行安装”  。 立即创建虚拟环境，确保它会从源代码管理中排除。 （始终可从 requirements.txt 创建该环境  。）

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>步骤 1-2：检查 Git 控件并发布到远程存储库

由于选择了“新建项目”  对话框中的“创建新的 Git 存储库”  ，在创建过程完成后，项目就已经提交到本地源代码管理。 在此步骤中，你将熟悉 Visual Studio 的 Git 控件和在其中使用源代码管理的“团队资源管理器”  窗口。

1. 在 Visual Studio 主窗口下角处检查 Git 控件。 这些控件从左到右依次显示未推送的提交、未提交的更改、存储库的名称以及当前分支：

    ![Visual Studio 窗口中的 Git 控件](media/flask/step01-git-controls.png)

    > [!Note]
    > 如果未选择“新建项目”  对话框中的”创建新 Git 存储库“  ，Git 控件将仅显示用于创建本地存储库的”添加到源代码管理“  命令。
    >
    > ![未创建存储库时 Visual Studio 中显示的“添加到源代码管理”](media/tutorials-common/step01-git-add-to-source-control.png)

1. 选择“更改”按钮，Visual Studio 会在“更改”  页上打开“团队资源管理器”  窗口。 由于新创建的项目已经自动提交给源代码管理，因此，看不到任何挂起的更改。

    ![“更改”页上的“团队资源管理器”窗口](media/flask/step01-team-explorer-changes.png)

1. 在 Visual Studio 状态栏中，选择“未推送的提交”按钮（标有“2”的向上箭头）以打开团队资源管理器中的“同步”页    。 由于你只有一个本地存储库，页面将提供简单的选项将存储库发布到不同的远程存储库。

    ![显示面向源代码管理的可用 Git 存储库选项的“团队资源管理器”窗口](media/flask/step01-team-explorer.png)

    可以为自己的项目选择任何所需的服务。 本教程演示了如何使用 GitHub，其中本教程已完成的示例代码保存在 [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask) 存储库中。

1. 选择任一“发布”  控件时，“团队资源管理器”  都将提示你输入详细信息。 例如，在发布本教程的示例时，必须首先创建存储库本身，在这种情况下，“推送到远程存储库”  选项将与存储库的 URL 结合使用。

    ![用于推送到现有远程存储库的团队资源管理器窗口](media/flask/step01-push-to-github.png)

    如果没有现有存储库，可通过“发布到 GitHub”  和“推送到 Azure DevOps”  选项直接从 Visual Studio 创建一个存储库。

1. 按照本教程执行操作时，请养成定期在 Visual Studio 中使用控件提交和推送更改的习惯。 本教程会在适当时机提醒你。

> [!Tip]
> 要在团队资源管理器中快速导航，请选择标头（上图中显示为“更改”或“推送”）来查看可用页面的弹出菜单    。

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>问：从项目一开始就使用源代码管理有什么好处？

答：首先，从一开始就使用源代码管理，特别是如果同时还使用远程存储库，就可以提供项目的常规异地备份。 与在本地文件系统上维护项目不同，源代码管理还提供了完整的更改历史记录，用户可以轻松地将单个文件或整个项目还原到以前的状态。 此更改历史记录有助于确定回归的原因（测试失败）。 此外，如果多个人员执行一个项目，则源代码管理必不可少，因为它管理重写并提供冲突解决方案。 最后，源代码管理从根本上来说是一种自动化形式，它为自动化构建、测试和发布管理提供充分准备。 这实际上是将 DevOps 用于项目的第一步，而且由于入门门槛非常低，因此没有理由不从一开始就使用源代码管理。

关于自动化形式的源代码管理的进一步讨论，请参阅 [The Source of Truth: The Role of Repositories in DevOps](https://msdn.microsoft.com/magazine/mt763232)（真相之源：DevOps 中的存储库角色），这是 MSDN Magazine 上专为移动应用编写的一篇文章，同样适用于 Web 应用。

### <a name="question-can-i-prevent-visual-studio-from-auto-committing-a-new-project"></a>问：我能否阻止 Visual Studio 自动提交新项目？

答：能。 若要禁用自动提交，请转到“团队资源管理器”  中的“设置”  页，选择“Git”   > “全局设置”  ，清除标记为“合并后默认提交更改”  的选项，然后选择“更新”  。

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>步骤 1-3：创建虚拟环境并从源代码管理中将其排除

你已为项目配置源代码管理，现在可以创建包含项目必需 Flask 包的虚拟环境。 然后，可以使用“团队资源管理器”  从源代码管理中排除环境文件夹。

1. 在“解决方案资源管理器”  中，右键单击“Python 环境”  节点并选择“添加虚拟环境”  。

    ![解决方案资源管理器中的“添加虚拟环境”命令](media/flask/step01-add-virtual-environment-command.png)

1. 随即出现“添加虚拟环境”对话框，并显示一条消息，指示“已找到 requirements.txt 文件   。” 此消息表示 Visual Studio 使用该文件来配置虚拟环境。

    ![包含 requirements.txt 消息的“添加虚拟环境”对话框](media/tutorials-common/step01-add-virtual-environment-found-requirements.png)

1. 选择“创建”  以接受默认设置。 （如果你愿意，可以更改虚拟环境名称，这只会更改其子文件夹的名称，但 `env` 是标准约定。）

1. 如果收到提示，同意管理员权限，然后在 Visual Studio 下载和安装包时耐心等待几分钟，对于 Flask 及其依赖项来说，这意味着在超过 100 的子文件夹中展开大约一千个文件。 可以在 Visual Studio“输出”  窗口中查看进度。 在等待时，仔细考虑下面的“问题”部分。 还可以在 [Flask 安装](https://flask.palletsprojects.com/en/1.0.x/installation/#installation)页 (flask.pcocoo.org) 上查看 Flask 依赖项的描述。

1. 在 Visual Studio Git 控件（位于状态栏上）上，选择更改指示器（显示“99&#42;”），这将打开团队资源管理器中的“更改”页    。

    创建虚拟环境带来了数百项更改，但不需要在源代码管理中包含其中任何一项，因为你（或克隆项目的任何人员）始终可从 requirements.txt 重新创建环境  。

    要排除虚拟环境，请右键单击 env 文件夹，然后选择“忽略这些本地项”   。

    ![忽略源代码管理更改中的虚拟环境](media/flask/step01-ignore-local-items.png)

1. 排除虚拟环境后，剩下的唯一更改是针对项目文件和 .gitignore  。 .gitignore 文件包含虚拟环境文件夹的附加条目  。 可以双击文件查看差异。

1. 输入提交消息，然后选择“全部提交”  按钮，根据需要将提交推送到远程存储库。

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>问：为什么需要创建虚拟环境？

答：虚拟环境是隔离应用确切依赖项的好办法。 此类隔离避免了全局 Python 环境中的冲突，有助于进行测试和协作。 随着时间的推移，在开发应用时，总是会引入许多有用的 Python 包。 通过将包保存在特定于项目的虚拟环境中，可以轻松更新项目中介绍该环境的 requirements.txt 文件，该文件包含在源代码管理中  。 如果项目被复制到任何其他计算机（包括生成服务器、部署服务器和其他开发计算机），仅使用 requirements.txt 即可轻松重新创建环境（这就是为什么环境不需要包含在源代码管理中）  。 有关详细信息，请参阅[使用虚拟环境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)。

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>问：如何删除已经提交给源代码管理的虚拟环境？

答：首先，编辑 .gitignore 文件以排除文件夹：在末尾找到带注释 *的部分，并为虚拟环境文件夹添加一个新行，如*`# Python Tools for Visual Studio (PTVS)``/BasicProject/env`。 （由于 Visual Studio 不会显示“解决方案资源管理器”  中的文件，请使用“文件”   > “打开”   > “文件”  菜单命令直接打开它。 也可以从团队资源管理器打开文件：在“设置”页上，选择“存储库设置”，转到“忽略和属性文件”部分，然后选择 .gitignore 旁的“编辑”链接。       ）

接下来，打开命令窗口，导航到包含虚拟环境文件夹（如 env）的文件夹（如 BasicProject），然后运行   `git rm -r env`。 然后从命令行 (`git commit -m 'Remove venv'`) 提交这些更改，或从“团队资源管理器”  的“更改”  页进行提交。

## <a name="step-1-4-examine-the-boilerplate-code"></a>步骤 1-4：检查样本代码

1. 项目创建完成后，在解决方案资源管理器中查看解决方案和项目，其中项目仅包含两个文件 app.py 和 requirements.txt    ：

    ![解决方案资源管理器中的空白 Flask 项目文件](media/flask/step01-blank-flask-project-in-solution-explorer.png)

1. 如前文所述，requirements.txt 文件指定 Flask 包依赖项  。 该文件旨在邀请你在第一次创建项目时创建虚拟环境。

1. 一个 app.py 文件包含三个部分  。 第一部分是 Flask `import` 语句，其作用是创建 `Flask` 类实例（分配给变量 `app`），然后分配 `wsgi_app` 变量（部署到 Web 主机时非常有用，但是现阶段暂不使用）：

    ```python
    from flask import Flask
    app = Flask(__name__)

    # Make the WSGI interface available at the top level so wfastcgi can get it.
    wsgi_app = app.wsgi_app
    ```

1. 第二部分（文件末尾）是一些可选代码，其作用是使用从环境变量中提取的特定主机和端口值（默认为 localhost:5555）启动 Flask 开发服务器：

    ```python
    if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555
        app.run(HOST, PORT)
    ```

1. 第三部分是将函数分配到 URL 路由的一些短代码，其作用是提供 URL 标识的资源。 使用 Flask 的 `@app.route` 修饰器定义路由，其参数是站点根目录中的相对 URL。 正如代码中所示，此处的函数仅返回文本字符串，已足够浏览器呈现。 在后面的步骤中，使用 HTML 呈现更丰富的页面。

    ```python
    @app.route('/')
    def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

### <a name="question-what-is-the-purpose-of-the-__name__-argument-to-the-flask-class"></a>问：name 参数对 Flask 类的作用是什么  ？

答：该参数是应用的模块或包名称，告知 Flask 查找属于应用的模板、静态文件和其他资源的位置。 对于单个模板中包含的应用，`__name__` 始终是正确值。 对需要调试信息的扩展也非常重要。 有关详细信息及其他参数，请参阅 [Flask 类文档](https://flask.palletsprojects.com/en/1.0.x/api/#flask.Flask) (flask.pocoo.org)。

### <a name="question-can-a-function-have-more-than-one-route-decorator"></a>问：一个函数能否有多个路由修饰器？

答：能，如果同一个函数服务于多个路由，则可以使用任意数量的修饰器。 例如，若要为“/”和“/hello”使用 `hello` 函数，请使用以下代码：

```python
@app.route('/')
@app.route('/hello')
def hello():
    """Renders a sample page."""
    return "Hello World!"
```

<a name="qa-url-variables"></a>

### <a name="question-how-does-flask-work-with-variable-url-routes-and-query-parameters"></a>问：Flask 如何使用变量 URL 路由和查询参数？

答：在路由中，使用 `<variable_name>` 标记任意变量，Flask 使用命名参数将参数传递到函数。 变量可以是 URL 路径的一部分或在查询参数中。 例如，`'/hello/<name>` 形式的路由将名为 `name` 的字符串参数生成到函数，在路由中使用 `?message=<msg>` 分析为“message=”查询参数提供的值并将其传递到 `msg` 等函数：

```python
@app.route('/hello/<name>?message=<msg>')
def hello(name, msg):
    return "Hello " + name + "! Message is " + msg + "."
```

若要更改类型，将变量前缀设为 `int`、`float`、`path`（接受斜杠来说明文件夹名称）和 `uuid`。 有关详细信息，请参阅 Flask 文档中的[变量规则](https://flask.palletsprojects.com/en/1.0.x/quickstart/#variable-rules)。

还通过 `request.args` 属性提供查询参数，特别是通过 `request.args.get` 方法。 有关详细信息，请参阅 Flask 文档中的[请求对象](https://flask.palletsprojects.com/en/1.0.x/quickstart/#the-request-object)。

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>问：在我安装其他包后，Visual Studio 能否从虚拟环境生成 requirements.txt 文件？

答：能。 展开“Python 环境”  节点，右键单击虚拟环境，并选择“生成 requirements.txt”  命令。 在修改环境，并将对 requirements.txt 所做的更改连同依赖于该环境的任何其他代码更改提交给源代码管理时，建议定期使用此命令  。 如果在生成服务器上设置持续集成，应该在修改环境时生成文件并提交更改。

## <a name="step-1-5-run-the-project"></a>步骤 1-5：运行项目

1. 在 Visual Studio 中，选择“调试” **“启动调试”(F5) 或使用工具栏上的“Web 服务器”按钮（所看到的浏览器可能会有所不同）**  >     ：

    ![Visual Studio 中的运行 Web 服务器工具栏按钮](media/tutorials-common/run-web-server-toolbar-button.png)

1. 任何一个命令将随机端口号分配到 PORT 环境变量，然后运行 `python app.py`。 代码使用 Flask 开发服务器中的端口启动应用。 如果 Visual Studio 显示“启动调试器失败”并显示无启动文件的相关消息，右键单击解决方案资源管理器中的 app.py 并选择“设为启动文件”     。

1. 服务器启动时，会打开一个控制台窗口，其中显示服务器日志。 然后，Visual Studio 自动将浏览器打开到 `http://localhost:<port>`，其中应该看到 `hello` 函数呈现的消息：

    ![Flask 项目默认视图](media/flask/step01-first-run-success.png)

1. 完成后，通过关闭控制台窗口，或使用 Visual Studio 中的“调试”   > “停止调试”  命令来停止服务器。

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>问：在项目 Python 子菜单中使用“调试”菜单命令和服务器命令有何区别？

答：除了“调试”  菜单命令和工具栏按钮之外，还可以使用项目上下文菜单上的“Python”   > “运行服务器”  或“Python”   > “运行调试服务器”  命令来启动服务器。 这两个命令都会打开一个控制台窗口，可以在其中看到运行服务器的本地 URL (localhost:port)。 但是，必须使用该 URL 手动打开浏览器，并且运行调试服务器不会自动启动 Visual Studio 调试器。 如果需要，稍后可以使用“调试”   > “附加到进程”  命令，将调试器附加到正在运行的进程。

## <a name="next-steps"></a>后续步骤

此时，基本 Flask 项目在同一个文件中包含启动代码和页面代码。 最好将这两个关注点分开，并且最好使用模板分离 HTML 和数据。

> [!div class="nextstepaction"]
> [使用视图和页面模板创建 Flask 应用](learn-flask-visual-studio-step-02-create-app.md)

## <a name="go-deeper"></a>深入了解

- [Flask 快速入门](https://flask.palletsprojects.com/en/1.0.x/quickstart/) (flask.pocoo.org)
- GitHub 上的教程源代码：[Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
