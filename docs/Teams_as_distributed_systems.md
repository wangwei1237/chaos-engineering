# 13.3 Teams as distributed systems
What’s a distributed system? Wikipedia defines it as “a system whose components are located on different networked computers, which communicate and coordinate their actions by passing messages to one another” (https://en.wikipedia.org/wiki/Distributed_computing). If you think about it, a team of people behaves like a distributed system, but instead of computers we have individual humans doing things and passing messages to one another.

Let’s imagine a team responsible for running customer-facing ticket-purchasing software for an airline. The team will need varied skills to succeed and because it’s a part of a larger organization, some of the technical decisions will be made for them. Let’s take a look at a concrete example of the core competences required for this team:

* Microsoft SQL database cluster management. That’s where all the purchase data lands and that’s why it is crucial to the operation of the ticket sales. This also includes installing and configuring Windows OS on VMs.
* Full-stack Python development. For the backend receiving the queries about available tickets as well as the purchase orders, this also includes packaging the software and deploying it on Linux VMs. Basic Linux administration skills are therefore required.
* Front-end, JavaScript-based development.
* Design. Providing artwork to be integrated into the software by the front-end developers.
* Integration with third-party software. Often, the airline can sell a flight operated by another airline, so the team needs to maintain integration with other airlines’ systems. What it entails varies from case to case.

Now, the team is made of individuals, all of whom have accumulated a mix of various skills over time as a function of their personal choices. Let’s say that some of our Windows DB admins are also responsible for integrating with third-parties (the Windows-based systems, for example). Similarly, some of the full stack developers also handle the integrations with Linux-based third-parties. Finally, some of the front-end developers can also do some design work. Take a look at figure 13.1, which shows a Venn diagram of these skills overlaps.

Figure 13.1 Venn diagram of skills overlap in our example team

![](../images/13.1.jpg)

The team is also lean. In fact, there are only six people on the team. Alice and Bob are both Windows and Microsoft SQL experts. Alice also supports some integrations. Caroline and David are both full stack developers, and both work on integrations. Esther is a front-end developer who can also do some design work. Franklin is the designer. Figure 13.2 places these individuals onto the Venn diagram of the skills overlaps.

Figure 13.2 Individuals on the Venn diagram of skills’ overlap

![](../images/13.2.jpg)

Can you see where I’m going with this? Just like with any other distributed system, we can identify the weak links by looking at the architecture diagram. Do you see any weak links? For example, if Esther has a large backlog, there is no one else on the team who can pick it up, because no one else has the skills. She’s a single point of failure. By contrast, if one of Caroline or David is distracted with something else, the other one can cover: they have redundancy between them. People need holidays, they get sick, and they change teams and companies, so in order for the team to be successful long term, identifying and fixing single points of failure is very important. It’s pretty convenient we had a Venn diagram ready!

One problem with real life is that it’s messy. Another is that teams rarely come nicely packaged with a Venn diagram attached to the box. Hundreds of different skills (hard and soft), constantly shifting technological landscape, evolving requirements, personnel turnaround and a sheer scale of some organizations are all factors in how hard it can be to ensure no single points of failure. If only there was a methodology to uncover systemic problems in a distributed system... Oh wait!

In order to discover systemic problems within a team, let’s do some chaos experiments! The following experiments are heavily inspired by Dave Rensin who described them in his talk, “Chaos Engineering for People Systems” (https://youtu.be/sn6wokyCZSA). I strongly recommend watching that talk. They are also best sold to the team as “games” rather than experiments. Not everyone wants to be a guinea pig, but a game sounds like a lot of fun and can be a team-building exercise if done right. You could even have prizes!

Let’s start with identifying single points of failure within a team.

## 13.3.1 Finding knowledge single points of failure: “Staycation”
To see what happens to a team in the absence of a person, the chaos engineering way of verifying it is to simulate the event and observe how they cope. The most lightweight variant is to just nominate a person and ask them to not answer any queries related to their responsibilities and work on something different than they had scheduled for the day. Hence, the name staycation. Of course, it’s a game, and should an actual emergency arise, it’s called off and all hands are on deck.

If the team continues working fine at full (remaining) capacity, that’s great. It means the team is doing a really good job of spreading knowledge. But chances are that there will be occasions where other team members need to wait for the person on staycation to come back, because some knowledge wasn’t replicated sufficiently. It could be some work in progress that wasn’t documented well enough, some area of expertise that suddenly became relevant, some tribal knowledge the newer people on the team don’t have yet, or any number of other reasons. If that’s the case, congratulations: you’ve just discovered how to make your team stronger as a system!

People are different, and some will enjoy games like this much more than others. You’ll need to find something that works for the individuals on your team. There is not a single best way of doing this; whatever works is fair game. Here are some other knobs to tweak in order to create an experience better tailored for your team:

* Unlike a regular vacation, where the other team members can predict problems and execute some knowledge transfer to avoid them, it might be interesting to run this game by surprise. It will simulate someone falling sick, rather than taking a holiday.
* You can tell the other team members about the experiment... or not. Telling them will have an advantage that they can proactively think about things they won’t be able to resolve without the person on staycation. Telling them only after the fact is closer to a real-life situation, but might be seen as distraction. You know your team, suggest what you think will work best.
* Choose your timing wisely. If the team is working hard to meet a deadline, they might not enjoy playing games that eat up their time. Or, if they are very competitive, they might like that, and with the higher number of things going on there might be more potential for knowledge sharing issues to arise.

Whichever way works for your team, this can be a really inexpensive investment with a large potential payout. Make sure you take the time to discuss the findings with the team, lest they might find the game unhelpful. Everyone involved is an adult and should recognize when there is a real emergency. But even if the game went too far, failing early is most likely better than failing late, just like with the chaos experiments we run in computer systems.

Let’s take a look at another variant, this time focusing not on absence, but on false information.

## 13.3.2 Misinformation and trust within the team: “Liar, liar”
In a team, information flows from one team member to another. There needs to be a certain amount of trust between the members for effective cooperation and communication, but also a certain amount of distrust, so that we double-check and verify things, instead of just taking them at face value. After all, to err is human.

We’re also complex human beings, and we can trust the same person more on one topic than a different one. That’s very helpful. You reading this book shows some trust in my chaos engineering expertise, but that doesn’t mean you should trust my carrot cake (the last one didn’t look like a cake, let alone a carrot!) And that’s perfectly fine, these checks should be in place so that wrong information can be eventually weeded out. We want that property of the team, and we want it strong.

“Liar, liar” is a game designed to test how well your team is dealing with false information circulating. The basic rules are simple: nominate a person who’s going to spend the day telling very plausible lies when asked about work-related stuff. Some safety measures: write down the lies, and if they weren’t discovered by others, straighten them out at the end of the day and in general be reasonable with them. Don’t create a massive outage by telling another person to click “delete” on the whole system.

What this has a potential to uncover are situations where other team members skip the mental effort of validating their inputs and just take what they heard at face value. Everyone makes a mistake, and it’s everyone’s job to reality-check what you heard before you implement it. Here are some ideas of how to customize this game:

* Choose the liar wisely. The more the team relies on their expertise, the bigger the blast radius, but also the bigger the learning potential.
* The liar’s acting skills are actually pretty useful here. If they can keep it up for the whole day, without spilling the beans, it should have a pretty strong wow effect with other team members.
* You might want to have another person on the team know about the liar, to observe and potentially step in if they think the situation might have some consequences they didn’t think of. At a minimum, the team leader should always know about this!

Take your time to discuss the findings within the team. If people see the value in doing this, it can be good fun. Speaking of fun, do you recall what happened when we injected latency in the communications with the database in chapter 4? Let’s see what happens when you inject latency into a team.

## 13.3.3 Bottlenecks in the team: “life in the slow lane”
The next game, “life in the slow lane,” is about finding who’s a bottleneck within the team, in different contexts. In a team, people share their respective expertise to propel the team forward. But everyone has a maximum throughput of what they can process. Bottlenecks form, where some team members need to wait for others before they can continue with their work. In the complex network of social interactions, it’s often difficult to predict and observe these bottlenecks, until they become obvious.

The idea behind this game is to add latency to a designated team member by asking them to take at least X minutes to respond to queries from other team members. By artificially increasing the response time, you will be able to discover bottlenecks more easily: they will be more pronounced, and people might complain about them directly! Here are some tips to ponder:

* If possible, working from home might be useful when implementing the extra latency. It limits the amount of social interaction and might make it a bit less weird.
* Going silent when others are asking for help is suspicious, might make you uncomfortable, and can even be seen as rude. Responding to the queries with something along the lines of, “I’ll get back to you on this, sorry I’m really busy with something else right now,” might help greatly.
* Sometimes resolving found bottlenecks might be the tricky bit. There might be policies in place, cultural norms or other constraints to take into account, but even just knowing about the potential bottlenecks can help planning ahead.
* Sometimes, the manager of the team will be a bottleneck in some things. It might require a little bit more of self-reflection and maturity to react to that, but it can provide invaluable insights.

So this one is pretty easy, and you don’t need to remember the syntax of tc to implement it! And since we’re on a roll, let’s cover one more. Let’s see how to use chaos engineering to test out your remediation procedures.

## 13.3.4 Testing your processes: “inside job”
Your team, unless it was started earlier today, has a set of rules to deal with problems. These rules might be well-structured and written down; might be tribal knowledge in the collective mind of the team; or like it’s the case for most teams, somewhere in between the two. Whatever they are, these “procedures” of dealing with different types of incidents should be reliable. After all, that’s what you rely on in the stressful times. Given that you’re reading a book on chaos engineering, how do you think we could test them out?

With a gamified chaos experiment, of course! I’m about to encourage you to execute an occasional act of controlled sabotage by secretly breaking some sub-system you reasonably expect the team to be able to fix using the existing procedures, and then sit and watch then fix it.

Now, this is a big gun, so here’s a few caveats:

* Be reasonable about what you break. Don’t break anything that would get you in trouble.
* Pick the inside group wisely. You might want to let the stronger people on the team in on the secret, and let them “help out” by letting the other team members follow the procedures to fix the issue.
* It might also be a good idea to send some people to training or a side project, to make sure that the issue can be solved even with some people out.
* Double-check that the existing procedures are up to date before you break the system.
* Take notes while you’re observing the team react to the situation. See what takes up their time, what part of the procedure is prone to mistakes, who might be a single point of failure during the incident.
* It doesn’t have to be a serious outage. It might be a moderate severity issue, which needs to be remediated before it becomes very serious.

If done right, this can be a very useful piece of information. It increases the confidence in the team’s ability to fix an issue of a certain type. And again, it’s much nicer to be dealing with an issue just after lunch, rather than at 2am.

Would you do an inside job in production? The answer will depend on many factors we covered earlier in the chapter on testing in production and on the risk/reward calculation. In the worst-case scenario, you create an issue that the team fails to fix in time, the game needs to be called off, the issue fixed. You learn that your procedures are inadequate and can take action on improving them. In many situations, this might be perfectly good odds.

There are infinite other games you can come up with by applying the chaos engineering principles to the human teams and interaction within them. My goal here was to introduce you to some of them to illustrate that human systems have a lot of the same characteristics as computer systems. I hope that I pricked your interest. Now, go forth and experiment with and on your teams!