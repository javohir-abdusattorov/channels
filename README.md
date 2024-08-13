## Channels - implementing MPSC channels with instructions from Jon Gjengset
---

#### Link to the video
Crust of Rust series by Jon Gjengset:
https://www.youtube.com/watch?v=b4mS5UPHh20&list=PLqbS7AVVErFiWDOAVrPt7aYmnuuOLYvOa&index=6

#### Idea
To understand how channels work and are implemented, tried to build one myself without using ```std::mpsc```. Implemented flavor is Asynchronous, meaning unbounded capacity. To ensure data safety across threads, used Arc and Mutex

#### Tools
- *VecDeque* - used as queue, not Vec because getting first element of Vec requires shifting. And VecDeque is more like LinkedList and keeps track of head and tail indexes of vector
- *Arc* and *Mutex* - to enable locking mechanism on queue. Only one thread can add or remove from queue at a time
- *Condvar* - used for waking up sleeping Receivers when new message arrives. When queue is empty Receiver thread will go to sleep, and will be waked up be one of Senders if new message arrives