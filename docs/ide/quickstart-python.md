---
title: 快速入门：使用 Visual Studio 创建 Python Web 应用
description: 在此快速入门教程中，利用 Visual Studio 和 Flask 框架在 Python 中生成简单的 Web 应用。
ms.date: 03/07/2019
ms.technology: vs-python
ms.topic: quickstart
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- python
- data-science
ms.openlocfilehash: cbb06ac800fd21e2354b04fb2e7e46306da7ed72
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180343"
---
# <a name="quickstart-create-your-first-python-web-app-using-visual-studio"></a>快速入门：使用 Visual Studio 创建第一个 Python Web 应用

在 5-10 分钟介绍“用作 Python IDE 的 Visual Studio”的简介中，你将基于 Flask 框架创建一个简单的 Python Web 应用程序。 你将通过介绍 Visual Studio 基本功能的单独步骤创建项目。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。 在安装程序中，请确保选择“Python 开发”工作负荷  。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。 在安装程序中，请确保选择“Python 开发”工作负荷  。

::: moniker-end

## <a name="create-the-project"></a>创建项目

以下步骤创建一个作为应用程序容器的空项目：

::: moniker range="vs-2017"
1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”  。

3. 在“新建项目”对话框右上角的搜索字段中输入“Python Web 项目”，在中间的列表中选择“Web 项目”，为项目命名（如“HelloPython”），然后选择“确定”    。

    ![新建项目对话框，其中选择了 Python Web 项目](media/quickstart-python-00-web-project.png)

    如果找不到 Python 项目模板，请运行 Visual Studio 安装程序，选择“更多”>“修改”，选择“Python 开发”工作负载，然后选择“修改”      。

    ![Visual Studio 安装程序中的 Python 开发工作负载](../python/media/installation-python-workload.png)

4. 新项目在“解决方案资源管理器”  的右窗格中打开。 项目此时已为空，因为它不含其他文件。

    ![显示新创建的空项目的解决方案资源管理器](media/quickstart-python-01-empty-project.png)
::: moniker-end

::: moniker range=">=vs-2019"
1. 打开 Visual Studio 2019。
2. 在开始屏幕上，选择“创建新项目”  。
3. 在“创建新项目”对话框中，在顶部的搜索字段中输入“Python web”，在中间列表中选择“Web 项目”，然后选择“下一步”    ：

    ![创建新项目屏幕，其中选择了 Python Web 项目](media/quickstart-python-00-web-project-2019a.png)

    如果找不到 Python 项目模板，请运行 Visual Studio 安装程序，选择“更多”>“修改”，选择“Python 开发”工作负载，然后选择“修改”      。

    ![Visual Studio 安装程序中的 Python 开发工作负载](../python/media/installation-python-workload.png)

4. 在接下来的“配置新项目”对话框中，输入“HelloPython”作为项目名称，指定一个位置，然后选择“创建”    。 （解决方案名称自动设置为匹配项目名称。   ）

    ![“配置新项目”对话框](media/quickstart-python-00-web-project-2019b.png)

5. 新项目在“解决方案资源管理器”  的右窗格中打开。 项目此时已为空，因为它不含其他文件。

    ![显示新创建的空项目的解决方案资源管理器](media/quickstart-python-01-empty-project-2019.png)
::: moniker-end

**问：在 Visual Studio 中为 Python 应用程序创建项目有何优势？**

**答**：通常只使用文件夹和文件定义 Python 应用程序，但如果程序变大，可能涉及到自动生成的文件和适用于 Web 应用程序的 JavaScript 等，这种简单的结构就变得很繁琐。 Visual Studio 项目帮助管理复杂性问题。 该项目（  .pyproj 文件）标识与项目关联的所有源文件和内容文件，包含每个文件的生成信息，维护这些信息并与源代码管理系统集成，并帮助你将应用程序组织为逻辑组件。

**问：解决方案资源管理器中显示的“解决方案”是指什么？**

**答**：Visual Studio 解决方案是一个容器，可帮助你将一个或多个相关项目作为一个组进行管理，并存储不特定于项目的配置设置。 解决方案中的项目还可相互引用，例如运行一个项目（Python 项目）会再自动生成一个项目（例如 Python 应用中使用的 C++ 扩展）。

## <a name="install-the-flask-library"></a>安装 Flask 库

Python 中的 Web 应用几乎总是使用众多可用 Python 库中的一个来处理低级别详细信息，如路由 Web 请求和调整响应。 为此，Visual Studio 为 Web 应用提供了各种模板，稍后我们将在快速入门中使用其中的一个模板。

在此按以下步骤将 Flask 库安装到 Visual Studio 用于此项目的默认“全局环境”。

::: moniker range="vs-2017"
1. 展开项目中的“Python 环境”  节点，查看项目的默认环境。

    ![显示默认环境的解决方案资源管理器](media/quickstart-python-02-default-environment.png)

2. 右键单击环境并选择“安装 Python 包”  。 此命令将打开“包”  选项卡上的“Python 环境”  窗口。

3. 在搜索字段中输入“flask”，再选择 [PyPI 中的“pip install flask”]  。 接受任何管理员权限提示，查看 Visual Studio 中的“输出”  窗口了解进度。 （当全局环境的包文件夹位于类似于 C:\Program Files  这样的受保护区域时，会出现提升提示。）

    ![使用 pip 安装，安装 Flask 库](media/quickstart-python-03-install-package.png)
::: moniker-end
::: moniker range=">=vs-2019"
1. 展开项目中的“Python 环境”  节点，查看项目的默认环境。

    ![显示默认环境的解决方案资源管理器](media/quickstart-python-02-default-environment-2019.png)

2. 右键单击环境并选择“管理 Python 包...”  。此命令将打开“包 (PyPI)”选项卡上的“Python 环境”窗口   。

3. 在搜索字段中输入"flask"。 如果 Flask 出现在搜索框下方，可跳过此步骤  。 否则选择“运行命令: pip install flask”  。 接受任何管理员权限提示，查看 Visual Studio 中的“输出”  窗口了解进度。 （当全局环境的包文件夹位于类似于 C:\Program Files  这样的受保护区域时，会出现提升提示。）

    ![使用 pip 安装，安装 Flask 库](media/quickstart-python-03-install-package-2019.png)
::: moniker-end

4. 安装完成后，库显示在“解决方案资源管理器”  的环境中，这意味着可以在 Python 代码中使用它。

    ::: moniker range="vs-2017"
    ![已安装 Flask 库并在解决方案资源管理器中显示](media/quickstart-python-04-package-installed.png)
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    ![已安装 Flask 库并在解决方案资源管理器中显示](media/quickstart-python-04-package-installed-2019.png)
    ::: moniker-end

> [!Note]
> 开发人员通常会创建一个虚拟环境用于安装特定项目的库，而不是在全局环境中安装库。 Visual Studio 模板通常会提供此选项，如[快速入门 - 使用模板创建 Python 项目](../python/quickstart-02-python-in-visual-studio-project-from-template.md)中所述。

**问：我可在何处深入了解其他可用的 Python 包？**

**答**：请访问 [Python 包索引](https://pypi.org/)。

## <a name="add-a-code-file"></a>添加代码文件

现已准备好添加一点 Python 代码来实现最小的 Web 应用。

1. 在“解决方案资源管理器”  中右键单击该项目，然后选择“添加”>“新建项”  。

1. 在出现的对话框中，选择“空 Python 文件”  ，将其命名为 app.py  ，然后选择“添加”  。 Visual Studio 会自动在编辑器窗口中打开该文件。

1. 复制以下代码，并将其粘贴到 app.py  ：

    ```python
    from flask import Flask

    # Create an instance of the Flask class that is the WSGI application.
    # The first argument is the name of the application module or package,
    # typically __name__ when using a single module.
    app = Flask(__name__)

    # Flask route decorators map / and /hello to the hello function.
    # To add other resources, create functions that generate the page contents
    # and add decorators to define the appropriate resource locators for them.

    @app.route('/')
    @app.route('/hello')
    def hello():
        # Render the page
        return "Hello Python!"

    if __name__ == '__main__':
        # Run the app server on localhost:4449
        app.run('localhost', 4449)
    ```

1. 你可能已注意到，“添加”>“新建项”  对话框显示了很多可添加到 Python 项目的其他类型的文件，例如 Python 类、Python 包、Python 单元测试和 web.config  文件等。 通常，可利用这些所谓的项模板通过有用的样本代码创建文件。

**问：我可在何处了解 Flask 的详细信息？**

**答**：请参阅 Flask 文档，首先是 [Flask 快速入门](https://flask.palletsprojects.com/en/1.1.x/quickstart/#quickstart)。

## <a name="run-the-application"></a>运行此应用程序

1. 在“解决方案资源管理器”中右键单击 app.py   ，然后选择“设置为启动文件”  。 此命令可标识运行应用时要在 Python 中启动的代码文件。

    ::: moniker range="vs-2017"
    ![在解决方案资源管理器中设置项目的启动文件](media/quickstart-python-05-set-as-startup-file.png)
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    ![在解决方案资源管理器中设置项目的启动文件](media/quickstart-python-05-set-as-startup-file-2019.png)
    ::: moniker-end

2. 右键单击“解决方案资源管理器”中的项目，再选择“属性”   。 然后选择“调试”  选项卡并将“端口号”  属性设置为 `4449`。 此步骤可保证 Visual Studio 启动带 `localhost:4449` 的浏览器与代码中的 `app.run` 参数进行匹配。

3.  依次选择“调试”和“开始执行(不调试)”  (Ctrl+F5  )，这会将更改保存至文件并运行应用。

4. 命令窗口中会显示消息“* 在 <https://localhost:4449/> 中运行”，随即打开指向 `localhost:4449` 的浏览器窗口应，显示“Hello, Python!”消息 状态为 200 的命令窗口中还显示 GET 请求。

    如果浏览器未自动打开，请启动所选的浏览器并导航到 `localhost:4449`。

    如果只在命令窗口中看到 Python 交互式 shell，或者如果该窗口在屏幕上短暂地闪烁，请确保在上述第 1 步中将 app.py  设为启动文件。

5. 导航到 `localhost:4449/hello`，测试确保 `/hello` 资源的修饰器也正常运行。 同样的，状态为 200 的命令窗口会显示 GET 请求。 随时可尝试其他 URL，查看它们是否在命令窗口中显示 404 状态代码。

6. 关闭命令窗口以停止应用，然后关闭浏览器窗口。

**问：“开始执行(不调试)”命令和“启动调试”有何区别？**

**答**：使用“启动调试”是在 [Visual Studio 调试器](../python/debugging-python-in-visual-studio.md)的上下文中运行应用，让你能够设置断点、检查变量和逐行执行代码  。 由于实现调试的挂钩各式各样，应用在调试器中的运行速度可能较慢。 与此相反，“开始执行(不调试)”直接运行应用，如同从命令行运行应用一样，但不调用上下文；而且此命令还自动启动浏览器并导航到项目属性的“调试”选项卡中指定的 URL   。

## <a name="next-steps"></a>后续步骤

祝贺你通过 Visual Studio 运行了第一个 Python 应用，这表示你初步了解了如何将 Visual Studio 用作 Python IDE！

> [!div class="nextstepaction"]
> [将应用部署到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)

此快速入门中的步骤比较笼统，你可能已猜到它们可以且应当自动执行。 此类自动化由 Visual Studio 项目模板执行。 浏览[快速入门 - 使用模板创建 Python 项目](../python/quickstart-02-python-in-visual-studio-project-from-template.md)获得演示，如何通过更少的步骤创建一个与本文创建的 Web 应用相类似的 Web 应用。

若要继续在 Visual Studio 中了解更完整的 Python 教程（包括使用交互式窗口、调试、数据可视化效果以及使用 Git），请浏览[教程：Visual Studio 中的 Python 入门](../python/tutorial-working-with-python-in-visual-studio-step-01-create-project.md)。

若要了解更多 Visual Studio 产品，请选择以下链接。

- 了解 [Visual Studio 中的 Python Web 应用模板](../python/python-web-application-project-templates.md)。
- 了解 [Python 调试](../python/debugging-python-in-visual-studio.md)
- 总括性地了解 [Visual Studio IDE](../get-started/visual-studio-ide.md) 的详细信息。
