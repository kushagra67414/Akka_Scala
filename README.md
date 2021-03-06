# AKKA LIBRARY USING SCALA !!!

## Day-1

* **@ AKKA, What it is ?** 
>A toolkit, integrate it without having to follow a source code layout. Akka helps us to focus on meeting business needs.  Akka provides Concurrency, Distribution, Fault tolerance out of the box Many programming models do not resolve the major problems associated with designing systems For modern computer architecture. Programming models must be fully distributed. Akka deals with many realities like Components get crashed without responding, messages get lost without a trace on the wire, and network latency fluctuates. So, Akka provides Multithreading, Transparent remote communication between systems and their components, A clustered, high-availability architecture that is elastic. It uses the actor model also gives you a vast set of tools that resolve the distributed/parallel system issues and provide everything where blends tightly and effectively together.


* **@ Why modern systems need a new approach of programming?**
> Earlier, Many Organization developing  the distributed system with the day to day challenges which can not be completely tackle by conventional object-oriented programming(OOPs) that’s why Actor model came into the existence which was proposed by the Carl Hewitt. “A way to manage the parallel processing in a high-performance Network”. Actor model is the reality of modern multi-threaded, multi-CPU architectures.
Actor model focus on the main issues like:
a.	The  Encapsulation Challenge
b.	An  illusion of shared memory on modern computer architectures
c.	The Illusion of a Stack of Call


* **@ The Actor Model Meets New, Distributed Systems Needs. How ?**
 Many programming models or practices do not fulfill the need of the modern distributed System. The actor model focuses on communication, not just the exchange of code that occurs between the organization. The Actor model crux on the supreme points which allow the structure to act in a manner that better suits our model best.

=> Actor fundamental unit of computation that embodies:
1. Processing
2.	Storage
3.	Communication


=> Advantage of Actor model as it allows to:

1.	Enforce encapsulation without resorting to locks.
2.	Use the cooperative entity model that responds to signals, changes state, and sends signals to each other to forward the entire application.
3.	Stop worrying about an executing mechanism that is a mismatch to our world view.


## Day-2

### @ Mechanism OF an ACTOR MODEL !!!

Actors send messages to each other instead of calling methods directly. Actors don’t contain the execution of the thread they just delegate the message from the sender to the destination without blocking and complete more at the same time.
The actor responds to the message and returns the execution when the current message is processed.
The actor acts as an object. Object invokes the method while the actor invokes the messages. Actors execute independently and also react to the incoming messages sequentially but actor different actors currently processing the messages work concurrently with each other which helps not to drive multiple threads into the actor or causing any destruction.
Here, Simply we can say the actor adds the messages in queue form, and the actor is scheduled and marks it to a ready state. The actor picks the message from the front of the queue and modifies it like an internal state and sends it to the other actors available and the actor gets unscheduled. This happens when the actor receives any message. After these messages go into the actor mailbox and the behavior of the actor is a  description of how the actor reacts to messages.
Actor states are immutable and non-shareable, data propagate through messages this is how modern memory hierarchy works. Also, message data is stored on a cached line while keeping the local state and data cached at the original core.

### @ Actor handling the error !!!

Since there is not a call stack in the actor model due to which we need to handle the error in a different way.
The first error, if the actor delegates the task to the other actor i.e delegate actor and it gets failed which may be because of validation issues or user-id didn’t exist etc. Here, the message is not damaged, the actor is the one containing the error. The actor reply to the messages to the sender of the message.
Second, when encountering any internal fault. The actor in the system is organized in a tree-like structure.
When the actor creates another actor became the parent actor of the new actor and if any actor fails or stopped the parent actor decide how  to act. Also if the parent actor stopped all the child actor present also get stopped.

## Day-3

### @ Akka modules and libraries overview 
* Remoting 
* Cluster 
* Cluster Sharding
* Cluster Singleton
* Persistence
* Distributed Data
* Streams 
* HTTP


The most common used library :

1.	 Remoting:
```
SBT
         val AkkaVersion = "2.6.10"
         libraryDependencies += "com.typesafe.akka" %% "akka-remote" % AkkaVersion
Maven
         <properties>
         <akka.version>2.6.10</akka.version>
         <scala.binary.version>2.13</scala.binary.version>
         </properties>
         <dependency>
         <groupId>com.typesafe.akka</groupId>
         <artifactId>akka-remote_${scala.binary.version}</artifactId>
         <version>${akka.version}</version>
         </dependency>
```

Remoting helps actors who reside on separate machines to share messages seamlessly. Though distributed as a JAR artifact, Remoting is more like a module than a library. Here patterns are the same on the remote system as we use in our local systems.

Some problems were also solved by the remoting:

1.	How to fix actor systems that reside on remote hosts
2.	How to handle the individual actor's performances on remote actor systems.
3.	How to turn messages to bytes on the wire.
4.	How to handle low level, network connexions (and reconnections) between hosts, identify crashed actor systems and hosts, all transparently.
5.	How to multiplex communications from an unrelated set of actors on the same network connection, all of them transparently.



..

2.	Cluster  =>

```
SBT
         val AkkaVersion = "2.6.10"
         libraryDependencies += "com.typesafe.akka" %% "akka-cluster-typed" % AkkaVersion
Maven
         <properties>
         <akka.version>2.6.10</akka.version>
         <scala.binary.version>2.13</scala.binary.version>
         </properties>
         <dependency>
         <groupId>com.typesafe.akka</groupId>
         <artifactId>akka-cluster-typed_${scala.binary.version}</artifactId>
         <version>${akka.version}</version>
         </dependency>
```
Here, We manage sets of systems in a regimented way, Remoting mainly used for addressing and communicating with components of the remote system. In Cluster we can organize the set of the system into a “meta-system” means tied the system together which helps to analyze, describing, generalizing, etc. 

Cluster solve’s many issues like:

1.	establish a group of actor structures (clusters) that can communicate with each other and accept each other as part of a cluster.
2.	distribute computations among the current set of members.
3.	How to detect devices that are momentarily unachievable reliably.
4.	How to delegate a certain function to the members of the cluster, in other words, to the delivery of certain services, not others.



..


3.	Cluster Sharding  =>

```
SBT
            val AkkaVersion = "2.6.10"
            libraryDependencies += "com.typesafe.akka" %% "akka-cluster-sharding-typed" % AkkaVersion
Maven
           <properties>
           <akka.version>2.6.10</akka.version>
           <scala.binary.version>2.13</scala.binary.version>
           </properties>
           <dependency>
           <groupId>com.typesafe.akka</groupId>
           <artifactId>akka-cluster-sharding-typed_${scala.binary.version}</artifactId>
           <version>${akka.version}</version>
           </dependency>
```




Cluster Sharding helps to resolve the issue of distributing a set of actors among the member of the Akka cluster. It helps a large set of persistent entities to members of a cluster to balance and migrate them to the other nodes when members crash.

Challenges that Cluster Sharding solves are:

*	How to model and scale-out a large set of stateful entities on a set of systems.
*	ensure that the entities in the cluster are correctly distributed such that the load is properly balanced across the devices.
*	ensure migrating entities from a crashed system without losing the state.
*	ensure that an entity does not exist on multiple systems at the same time and hence keeps consistent.


4.	Cluster Singleton  =>

```
SBT
          val AkkaVersion = "2.6.10"
           libraryDependencies += "com.typesafe.akka" %% "akka-cluster-singletone-typed" % AkkaVersion
Maven
          <properties>
          <akka.version>2.6.10</akka.version>
          <scala.binary.version>2.13</scala.binary.version>
          </properties>
          <dependency>
          <groupId>com.typesafe.akka</groupId>
          <artifactId>akka-cluster-singletone-typed_${scala.binary.version}</artifactId>
          <version>${akka.version}</version>
          </dependency>
```

A single entity is responsible for a particular job, which is shared with the other members of the cluster and migrated if the host system fails. This also creates bottleneck issues as it limits the scaling. Sometimes this pattern can be unavoidable too. A system that hosts a particular actor can be select by a cluster using Cluster Singleton.

This slove the many challenges like:
* One instance of a service run at a time in a whole cluster.
*	If the system hosting the services get crashed or shuts down services are still up and available
*	Step by step instructions to arrive at this occurrence from any individual from the group accepting that it can relocate to different systems over the long haul.


..

5.	Persistence  =>

```
SBT
      val AkkaVersion = "2.6.10"
       libraryDependencies += "com.typesafe.akka" %% "akka-persistence-typed" % AkkaVersion
Maven
      <properties>
      <akka.version>2.6.10</akka.version>
      <scala.binary.version>2.13</scala.binary.version>
      </properties>
      <dependency>
      <groupId>com.typesafe.akka</groupId>
      <artifactId>akka-persistence-typed_${scala.binary.version}</artifactId>
      <version>${akka.version}</version>
      </dependency>
```


Here, Actors also keep their state in volatile memory. So if our system gets crashed or deads the data will be completely lost. Persistent allows an actor to plow on events that lead to their current state. Upon initialization, events may be replayed to regain the status of the organization hosted by the actor.


Challenges Confronting:
*	Restoring the state of an actor.
*	Ensure stable messaging in the face of network failures and device crashes.
*	How to implement CQRS System
  * LINK: https://docs.microsoft.com/en-us/previous-versions/msp-n-p/jj591573%28v=pandp.10%29


..


6.	Distributed Data  =>

```
SBT
         val AkkaVersion = "2.6.10" 
         libraryDependencies += "com.typesafe.akka" %% "akka-cluster-typed" % AkkaVersion
Maven
         <properties>
         <akka.version>2.6.10</akka.version>
         <scala.binary.version>2.13</scala.binary.version>
         </properties>
         <dependency>
         <groupId>com.typesafe.akka</groupId>
         <artifactId>akka-cluster-typed_${scala.binary.version}</artifactId>
         <version>${akka.version}</version>
         </dependency>
```

This module provides an interface for data exchange and a variety of useful data types. This may achieve using CRDTs [Conflict Free Replicated Data Types ], where writes are done on different nodes and can happen at the same time and merge them afterward predictably.

This intends to resolve the challenges like =>

*	It accepts the writes on the nodes at cluster partition.
*	Also, low-latency while sharing data.


..


7.	Streams  =>

```
SBT
         val AkkaVersion = "2.6.10" 
         libraryDependencies += "com.typesafe.akka" %% "akka-stream-typed" % AkkaVersion
Maven
         <properties>
         <akka.version>2.6.10</akka.version>
         <scala.binary.version>2.13</scala.binary.version>
         </properties>
         <dependency>
         <groupId>com.typesafe.akka</groupId>
         <artifactId>akka-stream-typed_${scala.binary.version}</artifactId>
         <version>${akka.version}</version>
         </dependency>
```

It allows us to apply the same pattern over and over again. A scenario where graphs or a chain of actors needs to process potentially large sequential events and with proper resources so that the faster processing stages do not overpower the slower ones in the graph or chain of actors.

Challenges tackles =>

*	Handle large sequential events with high performance and proper resource usage.
*	Assemble reusable event/data processing parts
*	Link asynchronous services in a versatile way with high efficiency.
*	Uses in Reactive Streams standards which enables integrations with the third party.


..


8.	HTTP  =>

This is a separate module in akka i.e “AKKA_ HTTP”. This offers the HTTP-based services which also implements the full-server and client-side HTTPat top of the “akka-actor” and “akka-stream”. Akka HTTP makes build integration layer easier as allow to base your app. It is not a framework as provide maximum flexibility. Frameworks like PLAY, Lagom are based on akka.

Challenges tackeled =>

* Stream large dataset/evemts in and out of a system using HTTP.
