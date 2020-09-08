---
title: Docker 教程 - 第 8 部分：映像分层
description: 如何检查和管理 Docker 映像中的映像层。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: eae21a729f30a0c77fa52e5774a2f5157286dab1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89176671"
---
# <a name="image-layering"></a>映像分层

你是否知道你可以查看映像的组成部分？ 使用 `docker image history` 命令，可以查看用于创建映像的每个层的命令。

1. 使用 `docker image history` 命令，可查看在本教程前面部分创建的 `getting-started` 映像中的层。

    ```bash
    docker image history getting-started
    ```

    获得的输出应如下所示（日期/ID 可能不同）。

    ```plaintext
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
    f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
    a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
    9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
    b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
    <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
    <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
    ```

    每一行表示映像中的一个层。 此处，底部显示的是基本层，顶部显示的是最新的层。 使用此输出，还可以快速查看每个层的大小，帮助诊断大型映像的问题。

1. 可以发现，其中几行被截断。 如果添加 `--no-trunc` 标志，则可获得完整输出（是的，使用截断标志可获取未截断的输出）。

    ```bash
    docker image history --no-trunc getting-started
    ```

## <a name="layer-caching"></a>层缓存

现在，你已通过实际操作了解了分层，接下来有一个重要课程，介绍可如何缩短容器映像的生成时间。

> 层发生更改后，还必须重新创建所有下游层

让我们再次看看你正在使用的 Dockerfile…

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

返回到映像历史记录输出，可以看到，Dockerfile 中的每个命令都成为映像中的新层。 你可能还记得，在对映像进行更改时，必须重新安装 yarn 依赖项。 是否有解决此问题的方法？ 每次进行生成时都传送相同的依赖项没有什么意义，对吧？

要解决此问题，可以重新构建 Dockerfile，以帮助支持依赖项的缓存。 对于基于节点的应用程序，这些依赖项在 `package.json` 文件中定义。 那么，如果仅先复制该文件，安装依赖项，然后再复制其他所有内容，会发生什么情况？ 然后，仅在 `package.json` 发生更改时重新创建 yarn 依赖项。 这是否符合情理？

1. 先更新要在 `package.json` 中复制的 Dockerfile，安装依赖项，然后再复制其他所有内容。

    ```dockerfile hl_lines="3 4 5"
    FROM node:12-alpine
    WORKDIR /app
    COPY package.json yarn.lock ./
    RUN yarn install --production
    COPY . .
    CMD ["node", "/app/src/index.js"]
    ```

1. 使用 `docker build` 生成新映像。

    ```bash
    docker build -t getting-started .
    ```

    输出应如下所示…

    ```plaintext
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Running in d53a06c9e4c2
    yarn install v1.17.3
    [1/4] Resolving packages...
    [2/4] Fetching packages...
    info fsevents@1.2.9: The platform "linux" is incompatible with this module.
    info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
    [3/4] Linking dependencies...
    [4/4] Building fresh packages...
    Done in 10.89s.
    Removing intermediate container d53a06c9e4c2
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> a239a11f68d8
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 49999f68df8f
    Removing intermediate container 49999f68df8f
    ---> e709c03bc597
    Successfully built e709c03bc597
    Successfully tagged getting-started:latest
    ```

    可看到所有层都已重新生成。 这完全没问题，因为你已对 Dockerfile 进行了很多更改。

1. 现在，对 `src/static/index.html` 文件进行更改（例如将 `<title>` 更改为“令人惊叹的待办事项应用”）。

1. 现在，再次使用 `docker build` 生成 Docker 映像。 这次的输出看起来应该略有不同。

    ```plaintext hl_lines="5 8 11"
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> Using cache
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Using cache
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> cccde25a3d9a
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 2be75662c150
    Removing intermediate container 2be75662c150
    ---> 458e5c6f080c
    Successfully built 458e5c6f080c
    Successfully tagged getting-started:latest
    ```

    首先，可以发现生成速度要快得多！ 而且，还可看到步骤 1-4 均包含 `Using cache`。 太好了！ 你使用的是生成缓存。 推送和拉取此映像以及对其进行更新也将更快。 太好了！

## <a name="multi-stage-builds"></a>多阶段生成

虽然我们不会在本教程中深入探讨这一点，但多阶段生成是一种极为强大的工具，有助于通过多个阶段来创建映像。 它们有以下几个优点：

- 可将生成时依赖项与运行时依赖项分开
- 可通过仅传送应用需要运行的内容来减小整体映像大小

### <a name="maventomcat-example"></a>Maven/Tomcat 示例

生成基于 Java 的应用程序时，需要使用 JDK 将源代码编译为 Java 字节码。 但是，在生产环境中不需要 JDK。 此外，还可以使用 Maven 或 Gradle 等工具来帮助生成应用。
最终映像中也不需要这些工具。 多阶段生成将有所帮助。

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

此示例使用一个阶段（称为 `build`）通过 Maven 来执行实际的 Java 生成。 第二个阶段（从 `FROM tomcat` 开始）从 `build` 阶段复制文件。 最终映像只是要创建的最后一个阶段（可以使用 `--target` 标志来替代它）。

### <a name="react-example"></a>React 示例

在生成 React 应用程序时，需要使用 Node 环境将 JS 代码（通常为 JSX）、SASS 样式表等编译为静态 HTML、JS 和 CSS。 如果未执行服务器端呈现，则无需为生产版本使用 Node 环境。 为什么不在静态 nginx 容器中传送静态资源？

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

此处，你将使用 `node:12` 映像执行生成（最大化层缓存），然后将输出复制到 nginx 容器中。 很酷吧！

## <a name="recap"></a>概括

通过深入了解映像的构造方式，可以更快地生成映像并减少要传送的更改。 多阶段生成还有助于减小总映像大小，并通过将生成时依赖项与运行时依赖项分开来提高最终容器安全性。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [部署到云](deploy-to-cloud.md)