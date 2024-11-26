---
title: 3.5. 開発プロジェクトのビルド
description: 
published: true
date: 2024-11-26T11:08:25.211Z
tags: 
editor: markdown
dateCreated: 2024-11-26T11:07:07.465Z
---

## パッケージリポジトリとは？

- CI ツールで Maven を使ってビルドを実行し、その結果生成されたアーティファクトをリポジトリにデプロイする設定がされることが一般的であると。以下のようなものがある。
- Maven Central Repository:
  - Maven のデフォルトのリモートリポジトリで、広く使用されています。
    ここにアーティファクトを公開することで、他の開発者がそのアーティファクトを容易に利用できるようになります。
- Nexus Repository:
  - Sonatype が提供するリポジトリ管理ツールで、Maven や Gradle などのビルドツールで使用されるリポジトリを管理することができます。
    自社内で使用するプライベートなリポジトリを構築する場合に利用されます。
- GitHub Packages:
  - GitHub が提供するパッケージ管理サービスで、Maven 用のパッケージを管理することができます。
- AWS CodeArtifact:
  - AWS が提供するマネージドなパッケージ管理サービスで、Maven をはじめとするさまざまなビルドツールのアーティファクトを管理できます。

ref.
https://terasolunaorg.github.io/guideline/current/ja/ImplementationAtEachLayer/CreateProject.html#tomcat

## Tomcat のリソース機能

```xml
<Resources className="org.apache.catalina.webresources.StandardRoot">
<PreResources className="org.apache.catalina.webresources.DirResourceSet"
                base="/etc/foo/bar/"
                internalPath="/"
                webAppMount="/WEB-INF/lib" />
</Resources>
```

- base="/etc/foo/bar/": base 属性は、実際のファイルシステム上でリソースの元となるディレクトリのパスを指定します。この場合、/etc/foo/bar/ というパスにあるディレクトリがリソースとして使用されます。
- internalPath="/": internalPath 属性は、このディレクトリが内部的にどのパスとしてマウントされるかを指定します。この場合、/ と指定されているので、/etc/foo/bar/ の内容が Web アプリケーションのルートパス / として扱われます。
- webAppMount="/WEB-INF/lib": webAppMount 属性は、このリソースをどの URL パスにマウントするかを定義します。ここでは、/WEB-INF/lib パスにマウントされるため、/etc/foo/bar/ 内のファイルが Web アプリケーション内の /WEB-INF/lib パスで利用可能になります。
- 具体的には、例えば /etc/foo/bar/some-lib.jar のようなファイルが、Web アプリケーション内の WEB-INF/lib/some-lib.jar としてアクセス可能になります。

ref. https://terasolunaorg.github.io/guideline/current/ja/ImplementationAtEachLayer/CreateProject.html#tomcat

## AP サーバデプロイ手順

- Tomcat には、外部リソースをコンテキストパスに含めることができる。
- VirtualWebappLoader の拡張という方法もあったが、どうやら同じ？バージョン違いで、最近のやつはこれを使わないぽい。
- jar なら`WEB-INF/lib`に含める、xml なら`/WEB-INF/classes`に含めるとかができる。
- このおかげで外部への設定ファイルの切り出しが可能。

ref.
https://stackoverflow.com/questions/23143697/adding-external-resources-to-class-path-in-tomcat-8

### コンテキストパスとは？

- コンテキストパスは、Web アプリケーションが Tomcat 上でアクセスされるための URL のパス部分です。
- 例えば、http://localhost:8080/myapp/ のような URL があった場合、/myapp がその Web アプリケーションのコンテキストパスです。

```xml
<Context docBase="/path/to/myapp" path="/myapp" />
```

- ここで、docBase は実際の Web アプリケーションのディレクトリを指し、path はそのアプリケーションのコンテキストパス（URL パス）を指定しています。この例では、http://localhost:8080/myapp/ という URL でアクセスされます。
