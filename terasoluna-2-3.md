---
title: 【TERASOLUNA】2.3. はじめてのSpring MVCアプリケーション
description: 
published: true
date: 2024-11-20T12:06:45.225Z
tags: terasoluna, spring mvc
editor: markdown
dateCreated: 2024-11-20T11:31:03.707Z
---

## SpringMvcConfigとは？
- Spring MVCの設定を行うためのconfigクラス。
- `todo\src\main\java\com\example\todo\config\web\SpringMvcConfig.java`
- 以下のようにクラス定義となる。
```java
/**
 * Configure SpringMVC.
 */
@ComponentScan(basePackages = { "com.example.helloworld.app" }) // (2)
@EnableAspectJAutoProxy
@EnableWebMvc // (1)
@Configuration
public class SpringMvcConfig implements WebMvcConfigurer {

}
```

## @ComponentScanとは？
- 指定されたパッケージをスキャンし、そこに定義されているSpringコンポーネント（@Component、@Controller、@Service、@Repositoryなどが付与されたクラス）を自動的に検出し、Springのアプリケーションコンテキストに登録するための仕組み。

### @ComponentScanを使うメリットとは？
- 手動で@Beanを登録する場合メソッドごとに設定をしていかなければならない。
- 仮に@ComponentScanを使わない場合、いくつものController、Service、Repositoryクラスを管理するConfigクラスを用意して、1つずつ登録していかなければならない。
- そのような煩雑さをなくすのが@ComponentScanである。
- クラスに@Controllerなどを付与するだけで自動で検出され、Springコンテナに登録することができる。

## ViewResolverとは？
- ViewResolverがビュー名を解析し、対象のビューを決定する。
