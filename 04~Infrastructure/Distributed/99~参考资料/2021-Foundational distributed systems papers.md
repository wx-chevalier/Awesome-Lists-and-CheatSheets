> [Origin](http://muratbuffalo.blogspot.com/2021/02/foundational-distributed-systems-papers.html)

# Foundational distributed systems papers

I talked about [the importance of reading foundational papers](http://muratbuffalo.blogspot.com/2021/02/read-papers-not-too-much-mostly.html) last week. To followup, here is my compilation of foundational papers in the distributed systems area. (I focused on the core distributed systems area, and did not cover networking, security, distributed ledgers, verification work etc. I even left out distributed transactions, I hope to cover them at a later date.)

I classified the papers by subject, and listed them in chronological order. I also listed expository papers and blog posts at the end of each section.

# Time and State in Distributed Systems

[Time, Clocks, and the Ordering of Events in a Distributed System.](https://lamport.azurewebsites.net/pubs/time-clocks.pdf) Leslie Lamport, Commn. of the ACM, 1978.

[Distributed Snapshots: Determining Global States of a Distributed System.](https://lamport.azurewebsites.net/pubs/chandy.pdf) K. Mani Chandy Leslie Lamport, ACM Transactions on Computer Systems, 1985.

[Virtual Time and Global States of Distributed Systems.](https://pages.cs.wisc.edu/~remzi/Classes/739/Fall2016/Papers/mattern89.pdf) Mattern, F. 1988.

[Practical uses of synchronized clocks in distributed systems.](https://muratbuffalo.blogspot.com/2022/11/practical-uses-of-synchronized-clocks.html) B. Liskov, 1991.

### Expository papers and blog posts

[There is No Now](https://queue.acm.org/detail.cfm?id=2745385). Justin Sheehy, ACM Queue 2015

[Why Logical Clocks are Easy](https://queue.acm.org/detail.cfm?id=2917756). Carlos Baquero and Nuno Preguiça, ACM Queue 2016.

[Hybrid logical clocks](http://muratbuffalo.blogspot.com/2014/07/hybrid-logical-clocks.html)

[Logical clocks and Vector clocks modeling in TLA+/PlusCal](http://muratbuffalo.blogspot.com/2018/01/logical-clocks-and-vector-clocks.html)

# Impossibility results

[Coordinated Attack or Two Generals problem](https://en.wikipedia.org/wiki/Two_Generals'_Problem) is a fundamental impossibility in distributed systems. It started more of folks theorem, so instead of pointing to a paper, I provide a link to the wikipedia page.

[Impossibility of Distributed Consensus with One Faulty Process](https://groups.csail.mit.edu/tds/papers/Lynch/jacm85.pdf), Fischer, Lynch and Patterson, JACM, 1985

[Unreliable Failure Detectors for Reliable Distributed Systems](https://www.cs.utexas.edu/~lorenzo/corsi/cs380d/papers/p225-chandra.pdf), Tushar Deepak Chandra and Sam Toueg, Journal of the ACM, 1996.

[Harvest, Yield, and Scalable Tolerant Systems](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.24.3690&rep=rep1&type=pdf), Armando Fox, Eric A. Brewer, 1999

[CAP Twelve years later: How the rules have changed,](https://sites.cs.ucsb.edu/~rich/class/cs293b-cloud/papers/brewer-cap.pdf) Eric Brewer, 2012.

### Expository papers and blog posts

[A Brief Tour of FLP Impossibility](http://the-paper-trail.org/blog/a-brief-tour-of-flp-impossibility/)

[Paper summary: Perspectives on the CAP theorem](http://muratbuffalo.blogspot.com/2015/02/paper-summary-perspectives-on-cap.html)

# Consensus and state machine replication

[Viewstamped Replication: A New Primary Copy Method to Support Highly-Available Distributed Systems.](http://pmg.csail.mit.edu/papers/vr.pdf) B. Oki and B. Liskov. SOSP 1988

[Implementing Fault-Tolerant Services Using the State Machine Approach: a Tutorial](https://www.cs.cornell.edu/fbs/publications/smsurvey.pdf), Fred Schneider, 1990

[How to build a highly available system with consensus,](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.61.8330&rep=rep1&type=pdf) Butler Lampson, 1996

[The Part-Time Parliament (Paxos)](https://lamport.azurewebsites.net/pubs/lamport-paxos.pdf) Leslie Lamport, 1998. ([See context](https://www.microsoft.com/en-us/research/publication/part-time-parliament/))

[Practical Byzantine Fault Tolerance.](http://pmg.csail.mit.edu/papers/osdi99.pdf) Miguel Castro, Barbara Liskov. OSDI 1999.

[Chain Replication for Supporting High Throughput and Availability](https://www.cs.cornell.edu/home/rvr/papers/OSDI04.pdf). Robbert van Renesse and Fred B. Schneider, OSDI 2004.

[ZooKeeper: Wait-free coordination for Internet-scale systems](https://www.usenix.org/legacy/event/atc10/tech/full_papers/Hunt.pdf). Patrick Hunt, Mahadev Konar, Flavio P. Junqueira, Benjamin Reed, Usenix ATC 2010.

[Tango: Distributed Data Structures over a Shared Log](https://dl.acm.org/doi/10.1145/2517349.2522732), Mahesh Balakrishnan, Dahlia Malkhi, Ted Wobber, Ming Wu, Vijayan Prabhakaran, Michael Wei, John D. Davis, Sriram Rao, Tao Zou, Aviad Zuckk. SOSP 2013.

[There is more consensus in Egalitarian parliaments](https://dl.acm.org/doi/10.1145/2517349.2517350). Iulian Moraru, David G. Andersen, Michael Kaminsky, SOSP 2013.

[Flexible Paxos: Quorum intersection revisited.](https://arxiv.org/abs/1608.06696) Heidi Howard, Dahlia Malkhi, Alexander Spiegelman. 2016.

[WormSpace: A modular foundation for simple, verifiable distributed systems.](https://flint.cs.yale.edu/flint/publications/socc19.pdf) Ji-Yong Shin, Jieung Kim, Wolf Honore, Hernán Vanzetto, Srihari Radhakrishnan, Mahesh Balakrishnan, Zhong Shao, SOCC'19.

### Expository papers and blog posts

[In Search of an Understandable Consensus Algorithm.](https://raft.github.io/raft.pdf) Diego Ongaro, John Ousterhout, Usenix ATC, 2014.

[Paxos Made Moderately Complex](https://www.cs.cornell.edu/courses/cs7412/2011sp/paxos.pdf). Robbert Van Renesse and Deniz Altinbuken, ACM Computing Surveys, 2015.

[Consensus in the Cloud: Paxos Systems Demystified](https://cse.buffalo.edu/tech-reports/2016-02.orig.pdf). Ailidani Ailijiang, Aleksey Charapko, Murat Demirbas, 2016.

[Modeling Paxos and Flexible Paxos in Pluscal and TLA+](http://muratbuffalo.blogspot.com/2016/11/modeling-paxos-and-flexible-paxos-in.html)

[Dissecting performance bottlenecks of Paxos protocols.](http://muratbuffalo.blogspot.com/2019/07/dissecting-performance-bottlenecks-of.html)

# Distributed algorithms

[Self-stabilizing systems in spite of distributed control](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.93.314&rep=rep1&type=pdf), Edsgar W. Dijkstra, CACM 1974.

[The Drinking Philosophers Problem](https://www.cs.utexas.edu/users/misra/scannedPdf.dir/DrinkingPhil.pdf), K. M. Chandy, J. Misra, ACM TOPLAS 1984

[Sparse partitions](http://courses.csail.mit.edu/6.895/fall02/papers/Awerbuch/focs90.pdf), Baruch Awerbuch, David Peleg, FOCS 1990.

[Distributed reset](http://web.cse.ohio-state.edu/siefast/group/publications/distributed-reset.pdf), Anish Arora, Mohamed Gouda, 1994

[The Arrow Distributed Directory Protocol](http://cs.brown.edu/people/mph/DemmerH98/disc.pdf), Michael J. Demmer, M. Herlihy, DISC 1998.

### Expository papers and blog posts

[Dijkstra's stabilizing token ring algorithm](http://muratbuffalo.blogspot.com/2015/01/dijkstras-stabilizing-token-ring.html)

[Modeling the hygienic dining philosophers algorithm in TLA+](http://muratbuffalo.blogspot.com/2016/11/hygienic-dining-philosophers.html)

# Miscellaneous

[Hints for computer system design](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/acrobat-17.pdf), Butler Lampson, 1983

[The role of distributed state](https://courses.cs.washington.edu/courses/cse552/07sp/papers/distributed_state.pdf), John Ousterhout, 1990

[SEDA: An Architecture for Well-Conditioned, Scalable Internet Services](http://www.sosp.org/2001/papers/welsh.pdf). Matt Welsh, David Culler, and Eric Brewer, SOSP 2001

[Crash only software](http://usenix.org/events/hotos03/tech/full_papers/candea/candea.pdf), George Candea, Armando Fox, HotOS 2003

### Expository papers and blog posts

[Learning about distributed systems: where to start?](http://muratbuffalo.blogspot.com/2020/06/learning-about-distributed-systems.html)

# Cloud computing, big data storage/processing

[Lessons from Giant-Scale Services](https://courses.cs.washington.edu/courses/cse454/05sp/papers/GiantScale-IEEE.pdf). Eric A. Brewer, IEEE Internet Computing, 2001.

[MapReduce: Simplified Data Processing on Large Clusters](https://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf). Jeffrey Dean and Sanjay Ghemawat, OSDI 2004.

[Optimistic Replication](https://dsf.berkeley.edu/cs286/papers/optimistic-csur2005.pdf), Yasushi Saito and Marc Shapiro, 2005.

[Dynamo: Amazon’s Highly Available Key-Value Store](https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html). Giuseppe DeCandia, Deniz Hastorun, Madan Jampani, Gunavardhan Kakulapati, Avinash Lakshman, Alex Pilchin, Swaminathan Sivasubramanian, Peter Vosshall and Werner Vogels, ACM SIGOPS 2007.

[On designing and deploying Internet scale services](https://mvdirona.com/jrh/talksAndPapers/JamesRH_Lisa.pdf), James Hamilton, LISA 2007

[Life beyond Distributed Transactions: an Apostate's Opinion](https://www.ics.uci.edu/~cs223/papers/cidr07p15.pdf), Pat Helland, CIDR 2007.

[Conflict-free Replicated Data Types](https://hal.inria.fr/inria-00609399v2/document). Marc Shapiro, Nuno Preguiça, Carlos Baquero, Marek Zawirski, 2011.

[Consistency Analysis in Bloom: a CALM and Collected Approach](https://people.ucsc.edu/~palvaro/cidr11.pdf), Peter Alvaro, Neil Conway, Joseph M. Hellerstein, William R. Marczak, CIDR 2011.

[Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing](https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf). Matei Zaharia, Mosharaf Chowdhury, Tathagata Das, Ankur Dave, Justin Ma, Murphy McCauley, Michael J. Franklin, Scott Shenker, Ion Stoica. NSDI 2012.

[Tail at scale](https://cacm.acm.org/magazines/2013/2/160173-the-tail-at-scale/fulltext). Jeff Dean, Luiz Andre Barroso, Commn of the ACM, 2013.

[Spanner: Google’s Globally Distributed Database](https://dl.acm.org/doi/pdf/10.1145/2491245), ACM, 2013.

[TensorFlow: A System for Large-Scale Machine Learning](https://www.usenix.org/conference/osdi16/technical-sessions/presentation/abadi), OSDI 2016.

### Expository papers

[Above the Clouds: A Berkeley View of Cloud Computing](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2009/EECS-2009-28.pdf). Michael Armbrust, Armando Fox, Rean Griffith, Anthony D. Joseph, Randy H. Katz, Andrew Konwinski, Gunho Lee, David A. Patterson, Ariel Rabkin, Ion Stoica, Matei Zaharia, 2009.

[Cloud Programming Simplified: A Berkeley View on Serverless Computing](https://arxiv.org/abs/1902.03383), 2019.
