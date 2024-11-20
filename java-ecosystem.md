---
title: Java Ecosystem
description: Javaを理解する上で前提となる歴史やステークホルダーなどを整理
published: true
date: 2024-11-20T11:36:43.742Z
tags: 
editor: markdown
dateCreated: 2024-11-20T11:36:43.742Z
---

# Java Ecosystem
ドキュメントを読む前にJavaのエコシステムを理解するところから始める。以下について関係性を整理していく。
- JSR（Java Specification Requests）
- JEP（JDK Enhancement Proposals）
- Java SE
- Jakarta EE
- Eclipse Foundation
- Java Community Process (JCP)
- Oracke Corporation
- JDK
- OpenJDK

## JSRとJEPの関係とは？
- JEPは、主にJDKの改善を目的とした提案書で、JavaランタイムやJDKの新機能（JVMの改善、言語機能、ツールの改善など）を対象としている。
- JEPは、OpenJDKコミュニティ内で提案され、迅速にJDKに組み込まれる。
- JSRは、Javaプラットフォームの標準仕様を定義するための提案書で、主にJava SEやJakarta EEのような大規模な技術の仕様を対象としている。
- JSRは、JCP（Java Community Process）を通じて標準化される。
- JEPとJSRは相互に影響し合っており、JEPが提案する新機能が、後にJSRを通じて標準化されることがあり、また、JSRが策定した新しいAPIや仕様が、JEPとしてJDKに実装されることもある。
- あくまでこれらの文書は提案書であり、JCPを通じて標準化され、次リリースのJava SEやJakarta EEなどで仕様として定義される。

## Jakarta EEとは？
- Jakarta EEは、エンタープライズアプリケーション向けの仕様群（API）を定義しており、例えば、サーブレット（HTTPリクエスト処理）、EJB（エンタープライズJavaBeans）、JPA（Java Persistence API）、JMS（Java Message Service）など、さまざまなAPIが含まれている。
- 元々はJava EEという名前だったが、Eclipse Foundationによって移管されJakarta EEとなった。
- Jakarta EEは標準化されたフレームワークであり、複数の実装（例えば、WildFly、Payara、GlassFishなど）から選択可能。
- これによりJava開発者は特定のサーバーやライブラリに依存しないコードを書けるというメリットがある。
- 以下のようなものが含まれる：
  - Servlets（Webアプリケーションのリクエスト処理）
  - JSP（JavaServer Pages）
  - JPA（Java Persistence API）
  - EJB（Enterprise JavaBeans）
  - JMS（Java Message Service）
  - CDI（Contexts and Dependency Injection） など。

### なぜEclipse Foundationへ移管したのか？
- Java EEの移管は開発の透明性の向上、革新の加速、そしてオープンソースコミュニティの強化を目的としたもの。
- Oracleの商業追及、閉鎖的な環境などに批判が集まり、完全なオープンソース化を決断した。
- Eclipse Foundationは、もともとEclipse IDE（統合開発環境）で知られるオープンソースの非営利団体で、非常に活発で大規模な開発者コミュニティを有している。
- また、Eclipse Foundationは、オープンソースプロジェクトの管理に優れた実績があり、Javaコミュニティでも強い影響力を持っていた。
- そのためJava EEの移管先として適任とされた。

## Java SEとは？
- 基本的なライブラリ、コアAPI（例：`java.lang`, `java.util`, `java.io`など）が含まれている仕様。
- OracleがJava SEの各バージョン（例えば、Java 8, Java 11, Java 17など）を公式にリリースし、そのリリースサイクルを管理。
- OpenJDKなどがこの仕様を実装し、JRE（APIとJVMを含む）、コンパイラを含めた形で一般向けに提供する。

### Java SEの例
- コアAPI: 例えば、コレクションフレームワーク（List, Set, Map）、ファイルI/O（java.io, java.nio）、マルチスレッド、ネットワーキング（Socket、URL）、GUI（Swing、JavaFX）など、アプリケーションの基盤となる標準ライブラリを提供します。
- Javaランタイム: Javaアプリケーションを実行するためのJVM（Java Virtual Machine）やJRE（Java Runtime Environment）などが含まれます。

## OpenJDKとは？
- オープンソースプロジェクトとしてOpenJDKがJava SEの公式な実装である。
- OpenJDK自体はOracleがスポンサーだが、実際には多くの企業や開発者が参加するオープンソースプロジェクト。
- これにより、OracleはJava SEの開発を、OpenJDKコミュニティの一部として進める。
- OpenJDKコミュニティとは、Oracleを中心としたコミュニティである。

## JDKのバージョン管理とJava SEのバージョン
- JDKのバージョン管理は、Java SEのバージョンに対応している。
- 例えば、JDK 8はJava SE 8に対応し、JDK 11はJava SE 11に対応している。
- JDKの新しいリリースが、Java SEのバージョンに合わせて出される。

## Java SEとJakarta EEとの関係とは？
- Java SEは基本的なプラットフォームやランタイム環境を提供する一方で、Jakarta EEは企業向けのフレームワークやAPI群を提供する。
- Jakarta EEはJava SEを基盤にして動作する。
- すべてのJakarta EEアプリケーションは、Java SEが提供する基本的な機能やAPIに依存している。
- OracleはJava SE（Standard Edition）とJava EE（Enterprise Edition）の役割をより明確にした。
- これにより、OracleはJava SEの管理に集中することができる。
- Java EEを他の企業やコミュニティに任せることで、より迅速な開発と多様なパートナーシップが可能となった。

## Java SEとJSRとの関係とは？
- Java SEの各バージョンでは、特定のJSRが導入され、それらのJSRが新しいAPIや機能として標準化される。

## 例
- Java SE 8：JSR 335（ラムダ式とStream API）、JSR 310（Java Time API）など
- Java SE 9：JSR 376（モジュールシステム）、JSR 379（Java Platform, Standard Edition 9 API Specification）など

## Jakarta EEとSpringの関係とは？
- Springはフレームワークであり、独自の設計思想に基づいている。SpringはJava EEの多くの概念を取り入れているが、Spring自身の解釈と独自のAPIを提供。
- 基本的にはアプリケーションサーバーに依存せず、軽量なコンテナで動作させることが可能。
- Springは特に「軽量性」と「設定の簡便さ」に重点を置いており、Spring Bootのように設定を自動化する機能がある。
- Jakarta EEは従来、比較的「重厚」で設定が多いため、Springは設定の簡素化へのモチベーションがある。
- 後継という立ち位置で現在はJavaのエンタープライズアプリではデファクトスタンダードとなっている。
