# 10 Chaos in Kubernetes

This chapter covers:

* Quick introduction to Kubernetes
* Designing chaos experiments for software running on Kubernetes
* Killing subsets of applications running on Kubernetes to test their resilience
* Injecting network slowness using a proxy

It’s time to cover Kubernetes (https://kubernetes.io/). For anyone working in software engineering, it would have been really hard to not hear it mentioned at the very least. I personally had never seen an open-source project become so popular so quickly. I remember going to one of the first editions of KubeCon in London in 2016 to try to evaluate whether it was worth investing any time into this entire Kubernetes thing. Fast forward to 2020, and Kubernetes expertise is now one of the most demanded skills!

Kubernetes solves (or at least makes it easier to solve) a lot of problems that arise when running software across a fleet of machines. Its wide adoption indicates that it might be doing something right. But, like everything else, it’s not perfect and it adds its own complexity to the system--complexity that needs to be managed and understood, and one that lends well to the practices of chaos engineering.

Kubernetes is a big topic, so we’ll split it into three chapters:

1. This chapter: Chaos in Kubernetes
    1. Quick introduction to Kubernetes, where it came from and what it does.
    2. Setting up a test Kubernetes cluster. We’ll cover getting a mini cluster up and running because there is nothing like working on the real thing. If you have your own clusters you want to use, that’s perfectly fine too.
    3. Testing a real project’s resilience to failure. We’ll first apply chaos engineering to the application itself, to see how it copes with the basic types of failure we expect it to handle. We’ll set things up manually.
2. Chapter 11: Automating Kubernetes experiments
    1. Introducing a high-level tool for chaos engineering on Kubernetes.
    2. Using that tool to re-implement the experiments we set up manually in chapter 10 to teach you how to do it more easily.
    3. Designing experiments for an ongoing verification of SLOs. We’ll see how to set things up to automatically detect problems on live systems, for example when an SLO is breached.
    4. Designing experiments for the cloud layer. We’ll see how we can leverage cloud APIs to test how systems behave when machines go down.
3. Chapter 12: Under the hood of Kubernetes
    1. Understanding how Kubernetes itself works, and how to break it. This is where we dig deeper, and we test the actual Kubernetes components. We’ll cover the anatomy of a Kubernetes cluster and discuss various ideas for chaos experiments to verify our assumptions about how it handles failure.

My goal with these three chapters is to take you from a basic understanding of what Kubernetes is and how it works, all the way to knowing how things tick under the hood, and where the fragile points are and how chaos engineering can help with understanding and managing the way the system handles failure.

This is pretty exciting stuff, and I can’t wait to show you around! Like every good journey, let’s start ours with a story.