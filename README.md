# OSAssignment3(Question 1)

Part 1 
Why deadlocks can appear in this setup?
Deadlocks can appear as it is a circular setup. If all the phhilosophers pick up each fork with there being 5 in total only and 2 of them pick up the bowls, every other philosopher will be waiting for either 
the fork to come back around or the bowl for them. The resources can not be forcibly taken from the process or in this case the philosopher holding them.

Part 2
How does our code prevent from there being any deadlocks?
1. We used mutex locks in here where access to both bowls at the centre of the table is required. Mutex locks are required to acceess for any philosopher to get into the eating state.
2. The philosophers follow a protocol where they acquire the forks and bowl in a specific order, avoiding the possibility of circular wait. For instance, a philosopher first acquires the left fork, then the right fork, and finally attempts to acquire a bowl. This order is consistent across all philosophers.
3. The pthread_mutex_trylock function is used when attempting to acquire a lock on the bowls. This function attempts to lock the mutex but returns immediately if the lock is not available. By using pthread_mutex_trylock in a loop, the philosophers can avoid getting stuck in a deadlock if the desired bowl is not available. If the philosopher cannot acquire the bowl, it releases the acquired forks, thinks, and tries again.
4. After eating is complete, the philosopher releases the acquired forks and the bowl. This ensures that the resources are properly released, allowing other philosophers to acquire them.

Part 3
Commenting on how fair the code is in terms of how often a philosopher is able to get into the eating state?
The fairness of the implementation may not be ideal, as some philosophers are able to eat more frequently than others. Fairness in this context would mean that each philosopher has an equal opportunity to acquire the necessary resources (forks and bowls) and proceed with eating.
In the output, it's observed that some philosophers, such as Philosopher 0, Philosopher 2, and Philosopher 4(You can say that 3 philosophers out of the five eat quite frequently as the order may vary), are able to eat more frequently, while others, like Philosopher 1 and Philosopher 3, may have longer periods of thinking without getting a chance to eat.
The lack of fairness could be attributed to the use of the pthread_mutex_trylock function, which attempts to acquire a lock but does not guarantee fairness or ordering among competing threads. This non-blocking approach allows a philosopher to continue thinking if the required resources are not immediately available.
