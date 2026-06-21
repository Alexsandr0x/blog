---
title: "Basics of Concurrency and Parallelism in Python"
translationKey: "python-concurrent"
date: 2022-12-28
description: "An attempt to explain concurrency and parallelism using dogs as an analogy"
build:
  list: never
  render: always
---

This content was originally prepared for the multi-robot systems tribe of the robotics team [Project Neon]() in August 2022. The content is open to members, but I preferred to write a revised summary in this post.

I made the content more agnostic by removing the mobile robotics references. I hope this attempt to make the concepts of concurrency and parallelism easy to understand is effective for someone!


## What is Parallelization?

**Parallelization**, parallel programming, or parallel computing is the **way of solving commands within a computational environment at the same time**.

This procedure is very useful in many computing segments that need high performance or simply need to do several things at once.

For example, your computer right now performs several parallel actions: it is managing network packets arriving at your browser, and when you listen to music while playing a game, both pieces of software are performing completely different yet parallel roles.

**When we are programming simple code, it's no different** — sometimes we want our code to do more than one thing at a time, but with structured programming as we know it, that's not possible.

{{< figure src="/images/python-parallelism/serial-vs-parallel.png" caption="Serial and Parallel communication in networks is a great **parallel** for our discussion.">}}

Usually we program in a **serial** way, meaning commands have a logical, well-structured order, one at a time. When you apply several print commands in Python or any language, you can be sure they will always run in the same order.

Now, when we apply a parallel strategy, we can have commands running at the same time, independently.


## Parallelization vs Concurrency

To understand parallelization in practice, we need to understand two very important concepts: **Parallelization** and **Concurrency**. Here, we will make the word parallelization more restricted to a clear definition while introducing a new concept: concurrency.

Concurrency refers to processes that execute while competing for the same resource — that resource could be the computer's memory, for example. This competition can happen in a way where these processes take turns consuming that resource.

{{< figure src="/images/python-parallelism/concurrent-model.png">}}

Note that in the concurrent example, we have two tasks, A and B, both running at the same time. However, for one to be processed, the other must stop, making the total time to execute both tasks equal to A + B.

Parallelization refers to processes that execute simultaneously and independently, possibly sharing resources or not.

{{< figure src="/images/python-parallelism/parallel-model.png">}}

In the parallel example, execution can happen at the same time — in the image, running on different CPUs. Whenever two processes are independent, by definition, parallelization can be used. Whenever two processes share some resource and need to divide its use, we can use concurrency.


## Feeding Dogs

To reinforce this notion, we can use a playful concept: two dogs competing to eat from a single food bowl.

{{< figure src="/images/python-parallelism/parallel-dogs-2.png">}}

Considering the two dogs as processes and the food bowl as the resource to be disputed, the serial solution here is for dog C1 to eat first until its hunger is satisfied, and only then does C2 get its chance to eat.

You don't need experience caring for animals to understand that this approach has several problems, and the same is true in process orchestration. If the resource is time, C1 may take too long and not give C2 an opportunity; if the amount of food in the bowl is limited, C2 may go hungry.

{{< figure src="/images/python-parallelism/parallel-dogs-3.png">}}

As a concurrent alternative, we can have dogs C1 and C2 eat in intervals, governed by some rule, such as time (each eats for 1 minute and then gives access to the resource to the other, for example).

If the rule is well thought out, we avoid resource scarcity problems like running out of time.

{{< figure src="/images/python-parallelism/parallel-dogs-4.png">}}

Finally, we have the parallel solution, where both processes eat independently, but from the same resource.

## Hands-On: Dogs in Python!

Now that we understand what concurrency and parallelism are, let's reinforce these concepts once and for all by practicing them with Python!

For this, let's first design a class that will represent our dogs:

{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 dog.py>}}

With this code we can initialize different dogs so they feed from a variable `pot`. This variable will be a list with finite resources. Note that `food_necessary` is defined as 10, meaning that for our dog to be satisfied, it needs to eat at least 10 treats.

To understand this code before observing it in the serial, concurrent, and parallel scenarios, let's understand what happens when we make a dog eat.

{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 simple_use_dog.py >}}

This code will give us the following result:

{{< figure src="/images/python-parallelism/dog_example.gif">}}

This way, we know the behavior when the dog is alone — 10 treats to eat, and 10 in the bowl, simple enough.

Note that we have a rule where below 50% the dog can die of hunger! So if we have two dogs and 10 treats, we have exactly what's needed to feed them, but in serial programming this logic will always kill the second dog!

Now, if we have two dogs in serial code...

{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 double_dog.py>}}

{{< figure src="/images/python-parallelism/double_dog_example.gif">}}



## Python Threads as a Concurrent Solution

One solution for the case of two dogs competing for food is to have them eat using a concurrent strategy. One of Python's concurrent solutions is the `Thread` module. With it, we can create methods that will be executed concurrently and managed by Python between their switches. We won't have exact control over when a dog stops eating, but what Python will do is: whenever we use a thread pause command, such as `time.sleep`, it will check whether there's another thread ready to work while the other is sleeping.

For this, we need to make the while loop we created into a method we'll call `task`. The `Thread` object will receive this method as a parameter, and also receive the function's arguments in the positional argument `args`.

{{< gist Alexsandr0x bd7b86b51fd4faccff23793249a6d893 thread_dogs.py>}}

And with that we get...

{{< figure src="/images/python-parallelism/thread_dogs.gif">}}

*Perfectly balanced, as all things should be...*

It's important to say that the example achieved exactly 50% with the two threads alternating perfectly, but that won't always be the case — especially in a complex application where Python is managing so many other threads that will be competing for resources. But this small example already shows a case where concurrency is beneficial.

## And the Parallel Solution?

I had designed a parallel explanation for this content when I first created it, but I'm not entirely satisfied with it today. The parallel approach requires some complex concepts such as memory sharing and race conditions that perhaps deserve another place...

Maybe someday I'll revisit this content in a Part 2 of this post...

## References

This text was based on my own content for a class I prepared focused on freshmen at the robotics team of the Federal University of ABC. Which in turn was based mainly on ***Luciano Ramalho** - Fluent Python* and ***Shaw, A** - CPython internals: your guide to the Python 3 interpreter*.
