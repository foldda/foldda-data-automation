# A 'Breadboard' System For Software Projects

Dubbed "breadboard for software", Foldda Automation is a simple, easy-to-use component-based software framework for building fun, cheap, and instant applications.

<div align="center">
<img src="_Resources/foldda-breadboard.png" width="450" align="center">
</div>

## "Breadboard-Like" App-Building Operations 

A Foldda project (called a "solution") consists of a selection of components (called "handlers") that collectively follow a design and perform an application. In Foldda these components are physically packaged as file system folders, which can be flexibly arranged and connected using common OS operations such as drag-and-drop, so building a Foldda app is somewhat like a breadboard project except it's in the software space. This short video illustrates building and running an ETP pipeline with Foldda components.

video demo here

As seen in the video, app-building with Foldda software components does not require a vendor-specific tool such as an IDE, which means you can build or change a "Foldda app" from any _bare_ Windows computer. Foldda components and the component-hosting runtime are implemented based on the API hosted in this repo. 

## An Open Software Component Marketplace 

The ultimate goal of Foldda Automation API is to become the base of an open software component marketplace, where free and premium components from different vendors are made available for people to assemble apps without much effort. 

One key issue that needs to be addressed is defining "the boundary" of a component in a vendor-neutral way, so 1) it can be obtained in an open market, and 2) it can co-exist and collabrate with the other components in an app.




can be done without specialized tools, so you can freely make changes to a Foldda "app" on any computer. This contrasts with the other "no-code" app-dev frameworks where the components must exist within a vendor-specific IDE environment
An open software component computing eco-system requires two pieces of technology: the first is a universal, vendor-independent packaging of software components as we've just discussed and demonstrated; the second is a standard interface that allows software components to freely and meaningful exchange data - think a "universal plug" for components like the pins and pin-holes on a physical breadboard.

The Foldda Automation Framework defines such a "plug", that is, the interface based on which components would work and exchange data, and the rest of the repo is the reference implementation of vendor-neutral software components and runtime development based on the defined framework. 

## Charian - Universal Data Exchange

A Foldda runtime `needs to address the problem of defining and implementing the interface between the components - which can be potentially independently developed and have no assumed knowledge of one other. And that is another key piece of tech from Foldda - the Charian object serialization API.

With Charian, Foldda runtime has this real power which is that it allows plug-n-play of third-party developed handlers that would work with existing handlers without having to recompile the app. It means you can have a handler built to your specific requirements while taking advantage of the existing prebuilt handlers, which means ultimate flexibility and control. And when a newly developed handler combines with the existing handlers, it multiplies the number of possible apps that can be built.

This allows Foldda Runtime to function as "the (software) breadboard", i.e. it powers up, and connects the input and the output of, the handler modules. More technically speaking, it navigates through a Foldda solution's folder hierarchy, executes the instructions in each module's folder, and provides data exchange between connected modules. An example of Foldda runtime is the Foldda Windows app.

## Foldda Automation Framework API

The purpose of this repo is to assist developers to understand and develop Foldda compatible software components (or runtimes). In addition to the open-sourced Foldda Automation Framework API source code, it also hosts the source code of many open-source licensed handlers, that can be used in your projects as they are, but also serve as boilerplate for your further custom development. The "Developer Kit" project included in this repo is a simple reference runtime which can be used for the convenience of custom handler development.

# Foldda's Technical Architecture 

In a Foldda app, each folder encapsulates a specific function of a data-processing step, the parent-children relationship of the stacked folders defines the data flow of the processing.

<<A pic of Foldda program flow>>

When a Foldda app executes in a runtime, each module's logic (a specific data-process step) is turned into a process by the runtime, and the app's intended data-processing is performed sequentially as laid out by the folder's hierarchical structure.

<< foldda app execution with runtime >>

# Foldda Handler Explained - A Design Analogy

The framework is modeled as a factory processing line, where a worker (known as a "handler") takes items from an input bucket, processes them, and places the processed items (or other types of output) into an output bucket.

The Foldda "runtime" is the work environment for the workers, which includes providing the worker its input bucket, and output bucket, and, if applicable, passing the output from a worker to the next worker.

So in a Foldda handler, all it does is take data records from the provided input container, do the intended processing to these records, and then place the produced output to the provided output container. As defined by the framework, a Foldda handler would implement the IDataHandler interface - 

```csharp
  public interface IDataHandler
  {
      /// Setting up the data-handler "worker" with its config, and its input and output storage 
      void Setup(IConfigProvider config, IDataStore inputStorage, IDataStore ouputStorage);

      /// Typically runs a processing loop that processes the input records and saves the output records to the output storage.
      Task ProcessData(CancellationToken cancellationToken);
  }
```

## Framework API Overview

## Handlers

## Runtimes

### Developer Kit




