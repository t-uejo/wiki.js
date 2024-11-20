---
title: 【TERASOLUNA】2.3. はじめてのSpring MVCアプリケーション
description: 
published: true
date: 2024-11-20T11:47:25.542Z
tags: terasoluna, spring mvc
editor: markdown
dateCreated: 2024-11-20T11:31:03.707Z
---

## ViewResolverとは？
- ViewResolverがビュー名を解析し、対象のビューを決定する。
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