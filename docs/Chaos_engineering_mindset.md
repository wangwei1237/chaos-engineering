# 13.1 Chaos engineering mindset
Find a comfortable position, lean back, and relax. Take control of your breath and try taking in deep, slow breaths through your nose, and release the air with your mouth. Now, close your eyes and try to not think about anything. I bet you found that hard, thoughts just keep coming. Don’t worry, I’m not going to pitch to you my latest yoga and mindfulness classes (they’re all sold out for the year)!. I just want to bring to your attention that a lot of what you consider “you” is happening without your explicit knowledge. From the chemicals produced inside of your body to help process the food you ate and make you feel sleepy at the right time of the night to split-second, subconscious decisions on other people’s friendliness and attractiveness based on visual cues, we’re all a mix of rational decisions and rationalizing the automatic ones.

To put it differently, parts of what makes up your identity are coming from the general-purpose, conscious parts of the brain, while others are coming from the subconscious. The conscious brain is much like implementing things in software - easy to adapt to any type of problem, but more costly and slow. That’s opposed to the quicker, cheaper, and more-difficult-to-change logic implemented in the hardware.

One of the interesting aspects of this duality is our perception of risk and rewards. We are capable of making the conscious effort to think about and estimate risks, but a lot of this estimation is done automatically without even reaching the level of consciousness. And the problem is that some of these automatic responses might still be optimized for surviving in the harsh environments the early human was exposed to, and not doing computer science.

Chaos engineering mindset is all about estimating risks and rewards with partial information, instead of relying on the automatic responses and gut feelings. It requires doing things that feel counterintuitive at first, like introducing failure into computer systems, after a careful consideration of the risk-reward ratio. It necessitates a scientific, evidence-based approach, coupled with a keen eye for potential problems. In the rest of this chapter I will try to illustrate why.

{% hint style='info' %}
CALCULATING RISKS - THE TROLLEY PROBLEM

If you think that you’re good at risk mathematics, think again. You might be familiar with the Trolley problem (https://en.wikipedia.org/wiki/Trolley_problem). In the experiment, participants are asked to make a choice which will affect other people - either keep them alive, or not. There is a trolley barrelling down the tracks. Ahead, there are five people attached to the tracks. If the trolley hits them, they die. You can’t stop the trolley and there is not enough time to detach even a single person. However, you notice a lever, Pulling the lever will redirect the trolley to another set of tracks, which only has one person attached to it. What do you do?

You might think that most people would calculate that one person dying is better than five people dying, and pull the lever. But the reality is that most people wouldn’t do it. There is something about it that makes the basic arithmetics go out of the window.
{% endhint %}

Let’s take a look at the mindset of an effective chaos engineering practitioner, starting with failure.

## 13.1.1 Failure is not a maybe: it will happen
Let’s assume that we’re using good-quality servers. One way of expressing the quality of being “good quality” in a scientific manner is the mean time between failure (MTBF). For example, if the servers had a very long MTBF of 10 years, that means that on average, each of them would fail every 10 years. Or put differently, the probability of the machine failing today is 1/(10 years * 365.25 days in a year) ~= 0.0003, or 0.03%. If we’re talking about the laptop I’m writing these words on, I am only 0.03% worried it will die on me today.

The problem is that small samples like this give us a false impression of how reliable things really are. Imagine now a datacenter with 10,000 servers in it. How many servers can they expect to fail on any given day? It’s 0.0003 * 10,000 ~= 3. Even with a third of that, at 3333 servers, the number would be 0.0003 * 3,333 ~= 1. The scale of modern systems we’re building makes small error rates like this more pronounced, but as you can see you don’t need to be Google or Facebook to experience them.

Once you get a hang of it, multiplying percentages is fun. Here’s another example. Let’s say that you have a mythical, all-star team shipping bug-free code 98% of the time. That means, on average, that with a weekly release cycle, they will ship bugs more than once a year. And if your company has 25 teams like that, all 98% bug free, you’re going to have a problem every other week, again, on average.

In the practice of chaos engineering, it’s important to look at things from this perspective - a calculated risk - and to plan accordingly. Now, with these well-defined values and elementary school-level multiplication, we can estimate a lot of things and make informed decisions. But what happens if the data is not readily available, and it’s harder to put a number to it?

## 13.1.2 Failing early vs failing late
One common mindset blocker when starting with chaos engineering is that we might cause an outage that we would otherwise most likely get away with. We discussed how to minimize this risk in the chapter on testing in production, so now I’d like to focus on the mental part of the equation. The reasoning tends to be like this: “It’s currently working, its lifespan is X years, so chances are that even if it has bugs that would be uncovered by chaos engineering, we might not run into them within this lifespan.”

There are many reasons why a person might think this. The company culture could be punitive for mistakes. They might have had software running in production for years, and bugs were found only when it was being decommissioned. Or simply because they have low confidence in their (or someone else’s) code. And there may be plenty of other reasons.

A universal reason, though, is that we have a hard time comparing two probabilities we don’t know how to estimate. Because an outage is an unpleasant experience, we’re wired to overestimate how likely it is to happen. It’s the same mechanism that makes people scared of dying of shark attack. In 2019 two people died of shark attacks in the entire world (https://www.floridamuseum.ufl.edu/shark-attacks/trends/location/world/.) Given the estimated population of 7.5B people in June 2019 (https://www.census.gov/popclock/world) the likelihood of any given person dying from a shark attack that year was 1 in 3,250,000,000. But because people watched the movie Jaws, if interviewed in the street, they will estimate that likelihood very high.

Unfortunately, this just seems to be how we are. So instead of trying to convince people to swim more in shark waters, let’s change the conversation. Let’s talk about the cost of failing early versus the cost of failing late. In the best-case scenario (from the perspective of possible outages, not learning), chaos engineering doesn’t find any issues, and all is good. In the worst-case scenario the software is faulty. If we experiment on it now, we might cause the system to fail and affect users within our blast radius. We call this failing early. If we don’t experiment on it, it’s still likely to fail, but possibly much later on (failing late).

Failing early has a number of advantages:

* There are engineers actively looking for bugs, with tools at the ready to diagnose the issue and help fix it as soon as possible. Failing late might happen at a much less convenient time.
* The same applies to the development team. The further in the future from the code being written, the bigger the context switch the person fixing the bug will have to execute.
* As a product (or company) matures, usually the users expect to see increased stability and decreased number of issues over time.
* Over time, the number of dependent systems tends to increase.

But because you’re reading this book, chances are you’re already aware of the advantages of doing chaos engineering and failing early. The next hurdle is to get the people around you to see the light too. Let’s take a look at how to achieve that in the most effective manner.