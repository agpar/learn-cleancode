## Chapter 13: Concurrency

Writing clean concurrent programs is **hard**. 

Concurrency decouples *what* gets done from *when* it gets done. While hard, it is often necessary
for throughput or latency requirements. 

A number of myths pervade concurrent programming:

* Myth: Concurrency always improves performance. Actually, it *may* improve performance.
* Myth: Design need not change when writing concurrent programs. Actually, it usually has a huge
  impact on system design. Dropping in a few standard library thread-safe data structures is rarely
  sufficient.
* Myth: Understanding concurrency issues is not important if your framework (e..g. Django) handles
  it for you. Actually, concurrent updates and deadlocks are nearly always an issue.
* Myth: Concurrency is free. Actually, there's always some overhead (often very significant)
  involved.
* Myth: Concurrency is simple for simple problems. Actually, it's pretty much always complicated. 
* Myth: Concurrency bugs that only occur sometimes are not a big deal. Actually, they are likely
  critical issues, as bugs only occur when your code is unsafe.

Remember: **very surprising results can occur when multiple threads unsafely share data**, as even
simple code may compile to long byte code sequences and all shuffling of these sequences are
possible. 

Here are tips for dealing with the complexity of concurrency:

**Treat Concurrency Control As A Single Responsibility**. As much as possible, employ wrappers for
your business logic classes that implement your concurrency needs. If a class is "thread-aware" that
should be the only thing it's aware of. Your main logic should be implemented in "thread-ignorant"
code.

**Encapsulate Shared Data**. It's possible to protect shared data with locks and `synchonrized`, but
the more frequently this is done the easier it is to make mistakes. Thus it is important to be
vigorous in limiting the access to any data that will be shared with good encapsulation.

**Copy Data and Use Immutable Objects**. If you can *avoid* sharing data, by simply making copies of
the data  (even better, immutable copies) your threads need, you can save a lot of headaches. 

**Try To Make Independent Threads**. If you adopt a model where each thread receives all its input
at initialization, never shares data with any other threads, and simply returns its results, you can
get the benefits of concurrency with none of the data-sharing headaches.

**Use Standard Library Thread-Safe Objects When Available**. They will likely solve many of our
problems and be extremely efficient.

**Develop An Understanding Of Basic Concurrency Models**. Start with vocabulary:

* **Bounded Resource**: A finite resource whose limits must be considered, e.g. database
  connections, fixed length buffers.
* **Mutual Exclusion**: When only one thread can access a resource at a time.
* **Starvation**: When a thread is routinely blocked by other threads, to the point that concurrency
  performance suffers.
* **Deadlock**: When t1 holds resource a and is waiting for resource b and t2 holds resource b and
  is waiting for resource a. No progress can be made.
* **Livelock**: When threads are stuck in a cycle of requesting and releasing resources, failing to
  make significant (or any) progress. 

Some standard models:

* **Producer-Consumer**: Producers place tasks in a bounded queue, while consumers remove them and
  execute them. Operations on the queue are the primary synchronization point - producers must wait
  when the queue is full and consumers must wait when the queue is empty, each signaling the other
  when the conditions change.
* **Readers-Writers**: A shared resource for data storage and retrieval which is occasionally
  updated. A balancing act must be struck so that readers do not read half written information, and
  writers don't starve readers.
* **Dining Philosophers**: Threads need access to bounded resource to progress. I.e. n philosophers
  sit at a table, each with a fork to their left. A philosopher needs two forks to eat. If a
  philosopher uses a "grab one fork and hold on to it until the next one is available", deadlocks
  ensue. How to handle requesting, acquiring, releasing and contending over resources to avoid
  deadlocks and maximize throughput.

**Avoid Dependencies Between Synchronized Methods**. Each synchronized method/block is a single
lock. If they call between each other, subtle issues can arise. Moreover, if a class has multiple
synchronized methods, it's possible that the class is incorrect, as it's possible for two threads to
be reading/writing to the class. In these cases, it's best to adopt a *single* lock for the entire
class. The class can provide a single public method with a lock that does all relevant work, or
public locking and releasing methods for clients to lock and do what they need.

**Keep `synchronized` Sections Small**. They are exclusive locks after all.

**Keep Shutdown Procedures In Mind**. Stopping many threads gracefully is difficult, and a possible
area to introduce deadlocks. Consider this design challenge up front. 

**Testing Threaded Code** Presents multiple challenges. Some tips. 

* Write many tests for threaded code. 
* Don't ignore spurious failures in tests for threaded code, they are usually a warning that a
  painful concurrency error exists. 
* Get code working and tested in a non-threaded environment first. Tracking down standard logical
  and concurrency errors both at once is a pain.
* Make your concurrent code "pluggable": it should support various concurrency situations (one, two,
  n threads) and capable of interacting with test doubles that can simulate timing issues and
  failures. 
* Write performance tests for your threaded code, as tuning the number of threads will be a relevant
  issue.  
* Test on different platforms, as different CPUs can effect or make errors in concurrency logic more
  obvious. 
* Try to force failures in tests using `sleep()`, `wait()` and `yield()`. You can use aspect
  oriented frameworks to "jiggles" into your code to simulate thread timing irregularities. 
