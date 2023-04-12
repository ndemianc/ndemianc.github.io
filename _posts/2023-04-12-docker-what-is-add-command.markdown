---
layout: post
title:  What is the Docker ADD command
description:
date:   2023-04-12 00:31:46.882708 -0500
author: sdemian
image:  '/images/2023-04-12-docker-what-is-add-command.png'
tags:   [docker, devops, add, technology]
tags_color: '#477690'
featured: true
---
The `ADD` command copies new files, directories or remote file URLs from source <span class="code"><src></span> and adds them to the filesystem of the image at the destination <span class="code"><dest></span> path.

Multiple <span class="code"><src></span> resources may be specified but if they are files or directories, their paths are interpreted as relative to the source of the context of the build.

> The `ADD` command is used to copy files/directories into Docker filesystem of the image.

The `ADD` command copy data in **three different ways**:

- Copy files from the local storage to a destination in the Docker image.
- Copy a tarball archive from the local storage and extract it automatically inside a destination <span class="code"><dest></span> path in the Docker image.
- Copy files from a URL to a <span class="code"><dest></span> inside the Docker image.

![ADD Diagram]({{site.baseurl}}/images/2023-04-12-docker-what-is-add-command-diagram.png)

## Syntax

```bash
ADD <src> <dest>
```

- If <span class="code"><src></span> is a file, it is simply copied to the <span class="code"><dest></span> directory.
- If <span class="code"><src></span> is a directory, its contents are copied to the <span class="code"><dest></span>, but the directory itself is not copied.
- <span class="code"><src></span> can be either a tarball or the URL.
- <span class="code"><src></span> needs to be within the directory where the docker build command was run.
- You can specify multiple sources for on ADD command.

## Code

Recently I had a problem with Linux Debian tool **wkhtmltodpf** which in Debian Bulleye version comes as `QT unpatched` and there was a need to install a `QT patched` version of **wkhtmltodpf**

Patched version of **wkhtmltodpf** can be downloaded from [https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.bullseye_arm64.deb](https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.bullseye_arm64.deb)

Let's compose **Docker ADD command** for this:

```bash
ARG WKHTMLTOPDF_DEB=https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.bullseye_arm64.deb
ADD $WKHTMLTOPDF_DEB /code/wkhtmltopdf.deb
```

Later we will be using download file at `/code/wkhtmltopdf.deb` by **ADD** command like this:

```bash

RUN dpkg -i code/wkhtmltopdf.deb && \
  rm -rf code/wkhtmltopdf.deb &&
```

> When adding multiple <span class="code"><dest></span> files or directories, there must be a <span class="code">/</span> at the end of the destination directory.

The same syntax is followed for tarballs and URLs.

And this is it. Congratulations 🏆 on learning about <span class="code">Docker ADD command!</span>

<span class="code">Thank You!</span>