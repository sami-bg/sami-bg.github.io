SMs get oversubscribed with threads, meaning each SM gets assigned far more threads than it can handle (32:1). Each SM also has the capacity to execute instructions for multiple threads (yet still a subset of the total) at the same time.

This helps GPUs tolerate long-latency operations (e.g. memory access) by cycling which threads are currently being executed and which threads are idle (with zero overhead). When a warp is waiting on the result of a long-latency operation, another warp will be executed instead of waiting for that operation to resolve. This is called latency tolerance.

**Latency tolerance**: "filling the latency time of operations from some threads with work from other threads" (page 83)

**For example:** you visit the post office and have all your paperwork filled out. Someone in queue front of you does not have their paperwork filled out. Instead of the clerk waiting on the person to fill their paperwork, 'blocking' the rest of the queue, they can handle other customers while said person is filling their paperwork.

customer: warp
no-paperwork customer: long-latency operation warp
clerk: hardware execution unit (AKA SM)

[[Dynamic partitioning and occupancy]]