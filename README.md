JDBC Integration   ![Build Status](https://travis-ci.org/kamon-io/kamon-jdbc.svg?branch=master)
==========================

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/kamon-io/Kamon?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[ ![Download](https://api.bintray.com/packages/kamon-io/snapshots/kamon-jdbc/images/download.svg) ](https://bintray.com/kamon-io/snapshots/kamon-jdbc/_latestVersion)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-jdbc_2.11/badge.svg)](https://maven-badges.herokuapp.com/maven-central/io.kamon/kamon-jdbc_2.11)


The `kamon-jdbc` module brings bytecode instrumentation to trace jdbc-compatible database requests

The <b>kamon-jdbc</b> module requires you to start your application using the AspectJ Weaver Agent. Kamon will warn you
at startup if you failed to do so.

The bytecode instrumentation     provided by the `kamon-jdbc` module hooks into the JDBC API to automatically
start and finish segments for requests that are issued within a trace. This translates into you having metrics about how
the requests you are doing are behaving.

### Getting Started

Kamon scala module is currently available for Scala 2.10, 2.11 and 2.12.

Supported releases and dependencies are shown below.

| kamon      | status | jdk  | scala            
|:----------:|:------:|:----:|------------------
|  1.0.0 |   RC   | 1.8+ | 2.10, 2.11, 2.12


To get started with SBT, simply add the following to your `build.sbt` or `pom.xml`
file:

```scala
libraryDependencies += "io.kamon" %% "kamon-jdbc" % "1.0.0"
```

```xml
<dependency>
    <groupId>io.kamon</groupId>
    <artifactId>kamon-jdbc_2.12</artifactId>
    <version>1.0.0</version>
</dependency>
```


### Metrics ###

The following metrics will be recorded:

* __reads__: a histogram that tracks the reads requests latency (SELECT statement).
* __writes__: a histogram that tracks the writes requests latency (INSERT, UPDATE, and DELETE statements).
* __slows__: a simple counter with the number of measured slow requests.
* __errors__: a simple counter with the number of failures.

### Slow Requests ###

Requests that take longer to execute than the configured `kamon.jdbc.slow-query-threshold` can be processed by user-defined
`kamon.jdbc.DefaultSlowQueryProcessor`. The default processor logs a warning message

### Error Processor ###
Requests that error can be processed by user-defined `kamon.jdbc.SqlErrorProcessor`. The default processor logs an error message

### Configuration ###

```typesafeconfig
kamon {
  jdbc {
    slow-query-threshold = 2 seconds

    # Fully qualified name of the implementation of kamon.jdbc.SlowQueryProcessor.
    slow-query-processor = kamon.jdbc.DefaultSlowQueryProcessor

    # Fully qualified name of the implementation of kamon.jdbc.SqlErrorProcessor.
    sql-error-processor = kamon.jdbc.DefaultSqlErrorProcessor
  }
}
```
