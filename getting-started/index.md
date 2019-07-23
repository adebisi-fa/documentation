---
outputFileName: index.html
---

# Step 1 - Install, run, and write your first event

[!include[<Getting Started Intro>](~/getting-started/_intro.md)]

This first step covers installation and running Event Store, and writing your first event.

[!include[<Getting Started Install and run>](~/partials/_install-run.md)]

## Interacting with an Event Store Server

There are three ways to interact with Event Store:

1.  [With the Admin UI](~/server/admin-ui.md).
2.  [With the HTTP API](~/http-api/index.md).
3.  With a Client API, which you need to install first. Our documentation covers the [.NET Core client API](~/dotnet-api/index.md) and the [JVM client](https://github.com/EventStore/EventStore.JVM) but [others](~/getting-started/which-api-sdk.md) are available.

### [.NET Client](#tab/tabid-dotnet-client)

[Install the .NET Core client API](https://www.nuget.org/packages/EventStore.ClientAPI.NetCore/) using your preferred method, add it to your project:

```shell
dotnet add package EventStore.Client
```

And require it in your code:

```csharp
using EventStore.ClientAPI;
```

### [JVM Client](#tab/tabid-jvm-client)

[Add the JVM client](https://github.com/EventStore/EventStore.JVM#setup) using Maven:

```xml
<dependency>
    <groupId>com.geteventstore</groupId>
    <artifactId>eventstore-client_2.12</artifactId>
    <version>5.0.8</version>
</dependency>
```

And require it in your code:

```java
import eventstore.*;
```

* * *

## Connecting to Event Store

If you want to use the Admin UI or the HTTP API, then you use port `2113`. For example, <http://127.0.0.1:2113/> in your web browser, or `curl -i http://127.0.0.1:2113` for the HTTP API.

> [!TIP]
> The default username and password is `admin:changeit`

![The Admin UI Dashboard](~/images/es-web-admin-dashboard.png)

To use a client API, you use port `1113` and create a connection:

### [.NET Client](#tab/tabid-dotnet-client-connect)

When using the .NET client, you also need to give the connection a name.

[!code-csharp[getting-started-connection](../../EventStore.Samples.Dotnet/DocsExample/Program.cs?start=32&end=33)]

> [!NEXT]
> In this example we used the [`EventStoreConnection.Create()`](xref:EventStore.ClientAPI.EventStoreConnection.Create(System.String,System.String)) overloaded method but [others are available](xref:EventStore.ClientAPI.EventStoreConnection).

### [JVM Client](#tab/tabid-jvm-client-connect)

[!code-java[getting-started-connection](../../EventStore.Samples.Java/src/main/java/org/eventstore/sample//WriteEventExample.java?start=17&end=22)]

> [!NOTE]
> For our JVM examples we use [akka](https://akka.io), a toolkit for building highly concurrent and distributed JVM applications.

* * *

## Writing Events to an Event Stream

Event Store operates on a concept of Event Streams, and the first operation we look at is how to write to a stream. If you are Event Sourcing a domain model, a stream equates to an aggregate function. Event Store can handle hundreds of millions of streams, so create as many as you need.

If you post to a stream that doesn't exist, Event Store creates it before adding the events.

You can write events using the Admin UI by clicking the _Stream Browser_ tab, the _Add Event_ button, filling in the form with relevant values and clicking the _Add_ button at the bottom of the page.

![Creating an event with the Admin UI interface](~/images/getting-started-add-event.gif)

Open a text editor, copy and paste the following event definition, and save it as _event.json_.

[!code-json[getting-started-write-event-json](~/code-examples/getting-started/event.json "The contents of event.json")]

### [HTTP API](#tab/tabid-4)

Use the following cURL command, passing the name of the stream and the events to write:

[!code-bash[getting-started-write-event-request](~/code-examples/getting-started/write-event.sh?start=1&end=1)]

> [!NEXT]
> Read [this guide](~/http-api/creating-writing-a-stream.md) for more information on how to write events with the HTTP API.
>
> [!NOTE]
> You can also post events to the HTTP API as XML, by changing the `Content-Type` header to `XML`.

### [.NET API](#tab/tabid-5)

To use the .NET API, use the following method, passing the name of the stream, the version, and the events to write:

[!code-csharp[getting-started-write-event-request](../../EventStore.Samples.Dotnet/DocsExample/Program.cs?range=95)]

> [!NEXT]
> Read [this guide](~/http-api/creating-writing-a-stream.md) for more information on how to write events with the .NET API. We don't cover version checking in this guide, but you can read more in [the optimistic concurrency guide](~/dotnet-api/optimistic-concurrency-and-idempotence.md).

### [JVM Client](#tab/tabid-6)

To use the JVM Client, use the following method, passing the name of the stream, the version, and the events to write:

[!code-java[getting-started-connection](../../EventStore.Samples.Java/src/main/java/org/eventstore/sample/WriteEventExample.java?start=23&end=36)]

* * *

## Next Step

In this first part of our getting started guide you learned how to install and run Event Store and write your first event. The next part covers reading events from a stream.

-   [Step 2 - Read events from a stream and subscribe to changes](~/getting-started/reading-subscribing-events.md)
