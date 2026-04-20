# A Distributed Systems Reading List

This document contains various resources and quick definition of a lot of background information behind distributed systems. It is not complete, even though it is kinda sorta detailed. I had written it some time in 2019 when coworkers at the time had asked for a list of references, and I put together what I thought was a decent overview of the basics of distributed systems literature and concepts.

Since I was asked for resources again recently, I decided to pop this text into my blog. I have verified the links again and replaced those that broke with archive links or other ones, but have not sought alternative sources when the old links worked, nor taken the time to add any extra content for new material that may have been published since then.

It is meant to be used as a quick reference to understand various distsys discussions, and to discover the overall space and possibilities that are around this environment.

### Foundational theory

This is information providing the basics of all the distsys theory. Most of the papers or resources you read will make references to some of these concepts, so explaining them makes sense.

#### Models

##### In a Nutshell

There are three model types used by computer scientists doing distributed system theory:

1. synchronous models
2. semi-synchronous models
3. asynchronous models

A **synchronous model** means that each message sent within the system has a known _upper bound_ on communications (max delay between a message being sent and received) and the processing speed between nodes or agents. This means that you can _know_ for sure that after a period of time, a message was missed. This model is applicable in rare cases, such as hardware signals, and is mostly beginner mode for distributed system proofs.

An **asynchronous model** means that you have no upper bound. It is legit for agents and nodes to process and delay things indefinitely. You can never assume that a "lost" message you haven't seen for the last 15 years won't just happen to be delivered tomorrow. The other node can also be stuck in a GC loop that lasts 500 centuries, that's good.

Proving something works on asynchronous model means it works with all other types. This is expert mode for proofs and is even trickier than real world implementations to make work in most cases.

The **Semi-synchronous models** are the cheat mode for real world. There _are_ upper-bounds to the communication mechanisms and nodes everywhere, but they are often configurable and unspecified. This is what lets a protocol designer go "you know what, we're gonna stick a _ping_ message in there, and if you miss too many of them we consider you're dead."

You can't assume all messages are delivered reliably, but you give yourself a chance to say "now that's enough, I won't wait here forever."

Protocols like Raft, Paxos, and ZAB (quorum protocols behind etcd, Chubby, and ZooKeeper respectively) all fit this category.

#### Theoretical Failure Modes

The way failures happen and are detected is important to a bunch of algorithms. The following are the most commonly used ones:

1. Fail-stop failures
2. Crash failures
3. Omission failures
4. Performance failures
5. Byzantine failures

First, **Fail-stop failures** mean that if a node encounters a problem, everyone can know about it and detect it, and can restore state from stable storage. This is easy mode for theory and protocols, but super hard to achieve in practice (and in some cases impossible)

**Crash failures** mean that if a node or agent has a problem, it crashes and then never comes back. You are either correct or late forever. This is actually easier to design around than fail-stop in theory (but a huge pain to operate because redundancy is the name of the game, forever).

**Omission failures** imply that you give correct results that respect the protocol or never answer.

**Performance failures** assumes that while you respect the protocol in terms of the content of messages you send, you will also possibly send results late.

**Byzantine failures** means that anything can go wrong (including people willingly trying to break you protocol with bad software pretending to be good software). There's a special class of **authentication-detectable byzantine failures** which at least put the constraint that you can't forge other messages from other nodes, but that is an optional thing. Byzantine modes [are the worst](http://scholar.harvard.edu/files/mickens/files/thesaddestmoment.pdf).

By default, most distributed system theory assumes that there are no bad actors or agents that are corrupted and willingly trying to break stuff, and byzantine failures are left up to blockchains and some forms of package management.

Most modern papers and stuff will try and stick with either crash or fail-stop failures since they tend to be practical.

See [this typical distsys intro slide deck](https://ti.tuwien.ac.at/cps/teaching/courses/dependable_systems-ss08/dcs_slides/dcs-2007-p5.pdf) for more details.

#### Consensus

This is one of the core problems in distributed systems: how can all the nodes or agents in a system agree on one value? The reason it's so important is that if you can agree on _just one value_, you can then do a lot of things.

The most common example of picking a single very useful value is _the name of an elected leader_ that enforces decisions, just so you can stop having to build more consensuses because holy crap consensuses are painful.

Variations exist on what exactly is a consensus, including does everyone agree fully? (strong) or just a majority? (t-resilient) and asking the same question in various synchronicity or failure models.

Note that while classic protocols like Paxos use a leader to ensure consistency and speed up execution while remaining consistent, a bunch of systems will forgo these requirements.

#### FLP Result

##### In A Nutshell

Stands for _Fischer-Lynch-Patterson_, the authors of a 1985 paper that states that proper consensus where _all_ participants agree on a value is unsolvable in a purely asynchronous model (even though it is in a synchronous model) as long as any kind of failure is possible, even if they're just delays.

It's one of the most influential papers in the arena because it triggered a lot of other work for other academics to define what exactly is going on in distributed systems.

##### Detailed reading

- [original paper](https://groups.csail.mit.edu/tds/papers/Lynch/jacm85.pdf)
- [blog post review](https://www.the-paper-trail.org/post/2008-08-13-a-brief-tour-of-flp-impossibility/) ([archive](https://web.archive.org/web/20230603122927/https://www.the-paper-trail.org/post/2008-08-13-a-brief-tour-of-flp-impossibility/))

#### Fault Detection

Following FLP results, which showed that failure detection was kind of super-critical to making things work, a lot of computer science folks started working on what exactly it means to detect failures.

This stuff is hard and often much less impressive than we'd hope for it to be. There are _strong_ and _weak_ fault detectors. The former implies all faulty processes are eventually identified by all non-faulty ones, and the latter that only some non-faulty processes find out about faulty ones.

Then there are degrees of accuracy:

1. Nobody who has not crashed is suspected of being crashed
2. It's possible that a non-faulty process is never suspected at all
3. You can be confused because there's chaos but at some point non-faulty processes stop being suspected of being bad
4. At some point there's at least one non-faulty process that is not suspected

You can possibly realize that a strong and fully accurate detector (said to be _perfect_) kind of implies that you get a consensus, and since consensus is not really doable in a fully asynchronous system model with failures, then there are hard limits to things you can detect reliably.

This is often why _semi-synchronous_ system models make sense: if you treat delays greater than _T_ to be a failure, then you can start doing adequate failure detection.

[See this slide deck for a decent intro](https://www.inf.ed.ac.uk/teaching/courses/ds/slides1415/failure.pdf)

#### CAP Theorem

The CAP theorem was for a long while just a conjecture, but has been proven in the early 2000s, leading to a lot of eventually consistent databases.

##### In A Nutshell

There are three properties to a distributed system:

- **C**onsistency: any time you write to a system and read back from it, you get the value you wrote or a fresher one back.
- **A**vailability: every request results in a response (including both reads and writes)
- **P**artition tolerance: the network can lose messages

In theory, you can get a system that is both available and consistent, but only under synchronous models on a perfect network. Those don't really exist so in practice **P** is always there.

What the CAP theorem states is essentially that _given_ **P**, you have to choose either **A** (keep accepting writes and potentially corrupt data) _or_ **C** (stop accepting writes to save the data, and go down).

##### Refinements

CAP is a bit strict in what you get in practice. Not all partitions in a network are equivalent, and not all consistency levels are the same.

Two of the most common approaches to add some flexibility to the CAP theorem are the _Yield/Harvest_ models and _PACELC_.

_Yield/Harvest_ essentially says that you can think of the system differently: _yield_ is your ability to fulfill requests (as in uptime), and _harvest_ is the fraction of all the potential data you can actually return. Search engines are a common example here, where they will increase their _yield_ and answer more often by reducing their _harvest_ when they ignore some search results to respond faster if at all.

_PACELC_ adds the idea that eventually-consistent databases are overly strict. In case of network **P**artitioning you have to choose between **A**vailability or **C**onsistency, but **E**lse --when the system is running normally--one has to choose between **L**atency and **C**onsistency. The idea is that you can decide to degrade your consistency for availability (but only when you really need to), or you could decide to always forego consistency because you gotta go fast.

It is important to note that you _cannot_ beat the CAP theorem (as long as you respect the models under which it was proven), and anyone claiming to do so is often a snake oil salesman.

##### Resources

- [CAP visual proof](https://mwhittaker.github.io/blog/an_illustrated_proof_of_the_cap_theorem/)
- [You can't sacrifice partition tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/)
- [PACELC](https://en.wikipedia.org/wiki/PACELC_theorem)

There's been countless rehashes of the CAP theorem and various discussions over the years; the results are mathematically proven even if many keep trying to make the argument that they're so reliable it doesn't matter.

#### Message Passing Definitions

Messages can be sent zero or more times, in various orderings. Some terms are introduced to define what they are:

- _unicast_ means that the message is sent to one entity only
- _anycast_ means that the message is sent to any valid entity
- _broadcast_ means that a message is sent to all valid entities
- _atomic broadcast_ or _total order broadcast_ means that all the non-faulty actors in a system receive the same messages in the same order, whichever that order is
- _gossip_ stands for the family of protocols where messages are forwarded between peers with the hope that eventually everyone gets all the messages
- _at least once delivery_ means that each message will be sent once or more; listeners are to expect to see all messages, but possibly more than once
- _at most once delivery_ means that each sender will only send the message one time. It's possible that listeners never see it.
- _exactly once delivery_ means that each message is guaranteed to be sent and seen only once. This is a nice theoretical objective but quite impossible in real systems. It ends up being simulated through other means (combining _atomic broadcast_ with specific flags and ordering guarantees, for example)

Regarding ordering:

- _total order_ means that all messages have just one strict ordering and way to compare them, much like 3 is always greater than 2.
- _partial order_ means that some messages can compare with some messages, but not necessarily all of them. For example, I could decide that all the updates to the key `k1` can be in a total order regarding each other, but independent from updates to the key `k2`. There is therefore a _partial_ order between all updates across all keys, since `k1` updates bear no information relative to the `k2` updates.
- _causal order_ means that all messages that depend on other messages are received after these (you can't learn of a user's avatar before you learn about that user). It is a specific type of partial order.

There isn't a "best" ordering, each provides different possibilities and comes with different costs, optimizations, and related failure modes.

##### Idempotence

Idempotence is important enough to warrant its own entry. Idempotence means that when messages are seen more than once, resent or replayed, they don't impact the system differently than if they were sent just once.

Common strategies is for each message to be able to refer to previously seen messages so that you define an ordering that will prevent replaying older messages, setting unique IDs (such as transaction IDs) coupled with a store that will prevent replaying transactions, and so on.

See [Idempotence is not a medical condition](https://queue.acm.org/detail.cfm?id=2187821) for a great read on it, with various related strategies.

#### State Machine Replication

This is a theoretical model by which, given the same sequences of states and the same operations applied to them (disregarding all kinds of non-determinism), all state machines will end up with the same result.

This model ends up being critical to most reliable systems out there, which tend to all try to replay all events to all subsystems in the same order, ensuring predictable data sets in all places.

This is generally done by picking a leader; all writes are done through the leader, and all the followers get a consistent replicated state of the system, allowing them to eventually become leaders or to fan-out their state to other actors.

#### State-Based Replication

State-based replication can be conceptually simpler to state-machine replication, with the idea that if you only replicate the state, you get the state at the end!

The problem is that it is extremely hard to make this fast and efficient. If your state is terabytes large, you don't want to re-send it on every operation. Common approaches will include splitting, hashing, and bucketing of data to detect changes and only send the changed bits (think of `rsync`), [merkle trees](https://en.wikipedia.org/wiki/Merkle_tree) to detect changes, or the idea of a `patch` to source code.

### Practical Matters

Here are a bunch of resources worth digging into for various system design elements.

#### End-to-End Argument in System Design

Foundational practical aspect of system design for distributed systems:

- a message that is sent is not a message that is necessarily received by the other party
- a message that is received by the other party is not necessarily a message that is actually read by the other party
- a message that is read by the other party is not necessarily a message that has been acted on by the other party

The conclusion is that if you want anything to be reliable, you _need_ an end-to-end acknowledgement, usually written by the application layer.

- [Overview by the morning paper](https://blog.acolyer.org/2014/11/14/end-to-end-arguments-in-system-design/)
- [Actual paper](http://web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf)
- [Wikipedia page](https://en.wikipedia.org/wiki/End-to-end_principle)

These ideas are behind the design of TCP as a protocol, but the authors also note that it wouldn't be sufficient to leave it at the protocol, the application layer must be involved.

#### Fallacies of Distributed Computing

The fallacies are:

- The network is reliable
- Latency is zero
- Bandwidth is infinite
- The network is secure
- Topology doesn't change
- There is one administrator
- Transport cost is zero
- The network is homogeneous

Partial explanations on the [Wiki page](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing) or full ones in [the paper](https://www.researchgate.net/publication/322500050_Fallacies_of_Distributed_Computing_Explained).

#### Common Practical Failure Modes

In practice, when you switch from Computer Science to Engineering, the types of faults you will find are a bit more varied, but can map to any of the theoretical models.

This section is an informal list of common sources of issues in a system. See also [the CAP theorem checklist](https://ferd.ca/beating-the-cap-theorem-checklist.html) for other common cases.

##### Netsplit

Some nodes can talk to each other, but some nodes are unreachable to others. A common example is that a US-based network can communicate fine internally, and so could a EU-based network, but both would be unable to speak to each-other

##### Asymmetric Netsplit

Communication between groups of nodes is not symmetric. For example, imagine that the US network can send messages to the EU network, but the EU network cannot respond back.

This is a rarer mode when using TCP (although it has happened before), and a potentially common one when using UDP.

##### Split Brain

The way a lot of systems deal with failures is to keep a majority going. A split brain is what happens when both sides of a netsplit think they are the leader, and starts making conflicting decisions.

##### Timeouts

Timeouts are particularly tricky because they are non-deterministic. They can only be _observed_ from one end, and you never know if a timeout that is ultimately interpreted as a failure was actually a failure, or just a delay due to networking, hardware, or GC pauses.

There are times where retransmissions are not safe if the message has already been seen (i.e. it is not idempotent), and timeouts essentially make it impossible to know if retransmission is safe to try: was the message acted on, dropped, or is it still in transit or in a buffer somewhere?

##### Missing Messages due to Ordering

Generally, using TCP and crashes will tend to mean that few messages get missed across systems, but frequent cases can include:

- The node has gone down (or the software crashed) for a few seconds during which it missed a message that won't be repeated
- The updates are received transitively across various nodes. For example, a message published by service `A` on a bus (whether Kafka or RMQ) can end up read, transformed or acted on and re-published by service `B`, and there is a possibility that service `C` will read `B`'s update before `A`'s, causing issues in causality

##### Clock Drift

Not all clocks on all systems are synchronized properly (even using [NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol)) and will go at different speeds.

Using a timestamp to sort through events is almost guaranteed to be a source of bugs, even moreso if the timestamps come from multiple computers.

##### The Client is Part of the System

A very common pitfall is to forget that the client that participates in a distributed system is part of it. Consistency on the server-side will not necessarily be worth much if the client can't make sense of the events or data it receives.

This is particularly insidious for database clients that do a non-idempotent transactions, time out, and have no way to know if they can try it again.

##### Restoring from multiple backups

A single backup is kind of easy to handle. Multiple backups run into a problem called [consistent cuts](https://www.cs.cornell.edu/courses/cs5414/2010fa/publications/BM93.pdf) ([high level view](https://blog.mattchung.me/2021/02/13/distributed-system-snapshots-consistent-vs-inconsistent-cuts/)) and distributed snapshots, which means that not all the backups are taken at the same time, and this introduces inconsistencies that can be construed as corrupting data.

The good news is there's no great solution and everyone suffers the same.

#### Consistency Models

There are dozens different levels of consistency, all of which are documented on [Wikipedia](https://en.wikipedia.org/wiki/Consistency_model), by [Peter Bailis' paper on the topic](http://www.vldb.org/pvldb/vol7/p181-bailis.pdf), or overviewed by [Kyle Kingsbury post on them](https://aphyr.com/posts/313-strong-consistency-models)

- _Linearizability_ means each operation appears atomic and could not have been impacted by another one, as if they all ran just one at a time. The order is known and deterministic, and a read that started after a given write had started will be able to see that data.
- _Serializability_ means that while all operations appear to be atomic, it makes no guarantee about _which_ order they would have happened in. It means that some operations _might_ start after another one and complete before it, and as long as the isolation is well-maintained, that isn't a problem.
- _Sequential consistency_ means that even if operations might have taken place out-of-order, they will appear as if they all happened in order
- _Causal Consistency_ means that only operations that have a logical dependency on each other need to be ordered amongst each other
- _Read-committed_ consistency means that any operation that has been committed is available for further reads in the system
- _Repeatable reads_ means that within a transaction, reading the same value multiple times always yields the same result
- _Read-your-writes_ consistency means that any write you have completed must be readable _by the same client_ subsequently
- _Eventual Consistency_ is a kind of special family of consistency measures that say that the system can be inconsistent as long as it eventually becomes consistent again. _Causal consistency_ is an example of eventual consistency.
- _Strong Eventual Consistency_ is like _eventual consistency_ but demands that no conflicts can happen between concurrent updates. This is usually the land of _CRDTs_.

Note that while these definitions have clear semantics that academics tend to respect, they are not adopted uniformly or respected in various projects' or vendors' documentation in the industry.

#### Database Transaction Scopes

By default, most people assume database transactions are linearizable, and they tend not to be because that's way too slow as a default.

Each database might have different semantics, so the following links may cover the most major ones.

- [PostgreSQL](https://www.postgresql.org/docs/9.1/transaction-iso.html)
- [MySQL](https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html) (depends on the storage engine used)
- [Transact-SQL](https://docs.microsoft.com/en-us/sql/t-sql/statements/set-transaction-isolation-level-transact-sql?view=sql-server-2017) (most of Microsoft's products)
- [Oracle](https://docs.oracle.com/cd/E25178_01/server.1111/e25789/consist.htm)

Be aware that while the PostgreSQL documentation is likely the clearest and most easy to understand one to introduce the topic, various vendors can assign different meanings to the same standard transaction scopes.

#### Logical Clocks

Those are data structures that allow to create either total or partial orderings between messages or state transitions.

Most common ones are:

- [Lamport timestamps](https://en.wikipedia.org/wiki/Lamport_timestamps), which are just a counter. They allow the silent undetected crushing of conflicting data
- [Vector Clocks](https://en.wikipedia.org/wiki/Vector_clock), which contain a counter per node, incremented on each message seen. They can detect conflicts in data and on operations.
- [Version Vectors](https://en.wikipedia.org/wiki/Version_vector) are like vector clocks, but only change the counters on state variations rather than all event seens
- [Dotted Version Vectors](https://github.com/ricardobcl/Dotted-Version-Vectors) are fancy version vectors that allow tracking conflicts that would be perceived by the client talking to a server.
- [Interval Tree Clocks](https://github.com/ricardobcl/Interval-Tree-Clocks) attempts to fix the issues of other clock types by requiring less space to store node-specific information and allowing a kind of built-in garbage collection. It also has [one of the nicest papers ever](http://gsd.di.uminho.pt/members/cbm/ps/itc2008.pdf).

#### CRDTs

CRDTs essentially are data structures that restrict operations that can be done such that they can never conflict, no matter which order they are done in or how concurrently this takes place.

Think of it as the specification on how someone would write a distributed redis that was never wrong, but only left maths behind.

This is still an active area of research and countless papers and variations are always coming out.

- [The big original complete paper](https://hal.inria.fr/inria-00609399v1/document)
- [A decent intro](https://medium.com/@istanbul_techie/a-look-at-conflict-free-replicated-data-types-crdt-221a5f629e7e)
- [Another intro](https://medium.com/@amberovsky/crdt-conflict-free-replicated-data-types-b4bfc8459d26)
- [Challenges in synchronizing CRDTs in practice](https://blog.acolyer.org/2019/03/11/efficient-synchronisation-of-state-based-crdts/)

### Other interesting material

- [Databases Reviews by Kyle Kingsbury](https://aphyr.com/tags/jepsen)
- [This list of material is great](https://dancres.github.io/Pages/)
- [Leader Election Algorithms](https://www.ijcsmc.com/docs/papers/June2014/V3I6201466.pdf)
- [Raft](https://raft.github.io/) (easy protocol intro)
- [Paxos made simple](https://lamport.azurewebsites.net/pubs/paxos-simple.pdf)
- [Paxos](https://lamport.azurewebsites.net/pubs/lamport-paxos.pdf) (the part-time parliament)
- [Paxos made Live](https://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/papers/paper2-1.pdf) (google experience report in making paxos work)
- [Paxos variations](https://en.wikipedia.org/wiki/Paxos_)
- [ZAB](https://www.cs.cornell.edu/courses/cs6452/2012sp/papers/zab-ieee.pdf) (the zookeeper algorithm)
- [The Dynamo paper](http://www.allthingsdistributed.com/files/amazon-dynamo-sosp2007.pdf)

The bible for putting all of these views together is [Designing Data-Intensive Applications](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/) by Martin Kleppmann. Be advised however that everyone I know who absolutely loves this book are people who had a good foundation in distributed systems from reading a bunch of papers, and greatly appreciated having it all put in one place. Most people I've seen read it in book clubs with the aim get better at distributed systems still found it challenging and confusing at times, and benefitted from having someone around to whom they could ask questions in order to bridge some gaps. It is still the clearest source I can imagine for everything in one place.
