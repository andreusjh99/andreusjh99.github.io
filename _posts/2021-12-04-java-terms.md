---
layout: post
title:  Java terms you will be interested in learning
read: 5
post-image: /assets/images/posts/8_java_terms/post.jpeg
description: A brief rundown of terms in Java that may be confusing for some who are starting out with Java.
categories: software development
---

---

![](/assets/images/posts/8_java_terms/post.jpeg)

**Java** is a high-level, class-based, object-oriented programming language. It is described as a **Write-Once, Run-Anywhere (WORA)** language, meaning it is meant to be compiled only once, and will be able to be run on any platform.

This post is NOT about programming with Java. It is about terms that you may have come across but are not quite sure about while learning Java. In this post, I will provide a brief rundown of some of these Java terms to help you understand them:
- [Java Versions](#java-versions)
- [Java Runtime Environment (JRE)](#java-runtime-environment-jre)
- [Java Development Kit (JDK)](#java-development-kit-jdk)
- [Java Distributions](#java-distributions)
- [Java SE, EE, ME](#java-se-ee-me)

## Java Versions

Unlike many other programming languages, Java version strings can be confusing for some especially when they first started approaching Java. Some questions that popped to my mind when I first learned about this include:
- Does Java 1.8 mean Java 1?
- Why don't we see Java 2.x, Java 3.x etc., but Java 5.x, 6.x, etc.?
- Does that mean Java 1 skipped directly to Java 5?

<hr style="border-style: dashed">

Prior to Java 5, Java versions increased from `1.0` to `1.1`, `1.2`, `1.3` and `1.4`. Then came Java 5 which introduced a new versioning system, dropping the leading `1.` from `1.5`, giving us Java `5.0`. To quote the <a href="https://docs.oracle.com/javase/1.5.0/docs/relnotes/version-5.0.html" target="_blank">release notes</a> of Java 5, this change in versioning system is to better reflect the level of maturity and stability of this new Java version.

Despite the introduction of the new versioning system, the old versioning system was still used in concurrent. `Java 1.5.0` and `Java 5.0` hence mean the same version of Java. This continued on until Java 8. The old versioning system was finally dropped with the release of Java 9.

Update numbers are written in multiple ways given the different versioning systems. Java 8 update 311 can be written as `Java 1.8.0_311`, `Java 1.8.311`, `Java 8u311`, or `Java 8.311` --- all of which are equivalent.

## Java Runtime Environment (JRE)
Historically, you only need to download a **Java Runtime Environment (JRE)** if you only want to run a Java program. As the name suggests, this is a runtime environment. The JRE consists of a **Java Virtual Machine (JVM)**, the java command-line tool, etc. --- tools needed to run a Java program.

Up until Java 8, you are able to download a JRE on its own. Starting from Java 9, you are always downloading a [JDK](#java-development-kit-jdk).

## Java Development Kit (JDK)
To develop Java programs, you will need the **development kit (JDK)**. A JDK includes:
- everything the JRE has (JVM, command-line tool, etc.)
- the compiler (**javac**)
- other tools like **javadoc**, debugger (**jdb**), etc.

Up until Java 8, as mentioned, JRE can be downloaded on its own. The **Oracle** website (Oracle is Java's developer) offers JREs and JDKs as separate downloads, even though the JDK always included JRE in a separate folder.

Starting from Java 9, the distinction is gone. You always download a JDK, and there is no longer an explicit JRE folder in the directories of the JDK.

## Java Distributions
Java's source code lives in the <a href="https://openjdk.org/" target="_blank">OpenJDK project</a>. In practice, anyone could produce a build from that source code. However, certification is required for distributing it. There are a handful of vendors that actually create their own builds, get them certified and distribute them. For instance, Linux distributions have always offered their own builds.

**Oracle** produce and maintain two different builds - OpenJDK builds and **OracleJDK builds**. The biggest difference between the two is that while Oracle's OpenJDK builds are free for both personal and commercial use, you will need to pay to use Oracle JDK builds for commercial purposes. This is because Oracle JDK builds provide long-term support (LTS) by Oracle developers.

## Java SE, EE, ME
**Java SE (Standard Edition)** provides the core functionalities of Java.

**Java EE (Enterprise Edition)** provides many additional features, including WebSocket, JavaServer Pages, etc., allowing us to create larger and more scalable applications.

**Java ME (Micro Edition)** provides functionalities specific to applications for embedded and mobile devices.

## Conclusion
- From Java 5 to Java 8, two versioning systems coexist (`1.x.0` and `x.0`). Since Java 9, only `x.0` is used.
- JRE is a runtime environment for running a Java program, while JDK is a development kit needed to develop a Java program and includes the JRE.
- SE means standard edition; EE means enterprise edition; ME means micro edition.

---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>