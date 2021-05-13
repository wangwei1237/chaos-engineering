# 13.2 Getting the buy-in
In order to get your team from zero to chaos engineering hero, you need them to understand the benefits it brings. And in order for them to understand those benefits, you need to be able to communicate them clearly. There are typically two groups of people you’re going to be pitching to: your peers/team members and your management. Let’s start by looking at how to talk to the latter.

## 13.2.1 Management
Put yourself in your manager’s shoes. The more projects you’re responsible for, the more likely you are to be risk-averse. After all, what you want is to minimize the number of fires to extinguish, while achieving your long-term goals. And chaos engineering can help with that.

So in order to play some music to your manager's ears, perhaps don’t start with breaking things on purpose in production. Here are some elements they are much more likely to react well to:

* Good return on investment (ROI): chaos engineering can be a relatively cheap investment (even a single engineer can experiment on a complex system in a single-digit number of days if the system is well documented) with a big potential pay off. The result is a win-win situation:
    * If the experiments don’t uncover anything, the output is twofold. First increased confidence in the system. Second, a set of automated tests which can be re-run to detect any regressions later.
    * If the experiments uncover a problem, it can be fixed.
    * Controlled blast radius: it’s good to remind them again, that this is not going to be randomly breaking things, but a well-controlled experiment, with a defined blast radius. Obviously, things can still go sideways, but the idea is not to set the world on fire and see what happens. Rather, it’s to take a calculated risk for a large potential pay off.
* Failing early:
    * Cost of resolving an issue found earlier is generally lower than if the same issue was found later.
    * Faster response time to an issue found on purpose, rather than at an inconvenient time.
* Better-quality software:
    * Your engineers knowing the software will get experimented are more likely to think about the failure scenarios early in the process and write more resilient software.
    * Team building: the increased awareness of the importance of interaction and knowledge sharing has the potential to make teams stronger. More on this later in this chapter.
* Increased hiring potential:
    * A real-life proof of building solid software. All companies talk about the quality of their product. Only a subset puts their money where their mouth is when it comes to funding engineering efforts in testing.
    * Solid software means fewer calls outside of working hours, which means happier engineers.
    * Shininess factor. Using the latest techniques helps attract engineers who want to learn them and have them on their CVs.

If delivered correctly, the tailored message should be an easy sell. It has the potential to make your manager’s life easier, make the team stronger, the software better quality, and hiring easier. Why would you not do chaos engineering?!

How about your team members?

## 13.2.2 Team members
When speaking to your team members, many of the arguments we just covered apply in an equal measure. Failing early is less painful than failing later, thinking about corner cases and designing all software with failure in mind is often interesting and rewarding. Oh and office games (we’ll get to them in just a minute) are fun.

But often what really resonates with the team is simply the potential of getting called less. If you’re on an on-call rotation, everything that minimizes the number of times you’re called in the midst of a night is helpful. So framing the conversation around this angle can really help with getting them onboard. Here are some ideas of how to approach that conversation:

* Failing early and during work hours: If there is an issue, it’s better to trigger it before you’re about to go pick up your kids from school or go to sleep in the comfort of your own home.
* Destigmatising failure: Even for a rock-star team, failure is inevitable. Thinking about it and actively seeking problems can remove or minimize the social pressure of not failing. Learning from failure always trumps avoiding and hiding failure. Conversely, for a poorly performing team, the failure is likely a common occurrence. Chaos engineering can be used in pre-production stages as an extra layer of testing, allowing the unexpected failures to be more rare.
* Chaos engineering is a new skill, and one that’s not that hard to pick up: Personal improvement will be a reward in itself for some. And it’s a new item on a CV.

With that, you should be well-equipped to evangelize chaos engineering within your teams and to your bosses. You can now go and spread the good word! But before you go, let me give you one more tool. Let’s talk about game days.

## 13.2.3 Game days
You might have heard of teams running game days. Game days are a good tool for getting the buy-in from the team. They are a little bit like those events at your local car dealership. Big, colorful balloons, free cookies, plenty of test drives and miniature cars for your kid, and boom--all of a sudden you need a new car. It’s like a gateway drug, really.

Game days can take any form. The form is not important. The goal is to get the entire team to interact, brainstorm some ideas of where the weaknesses of the system might lie, and have some fun with chaos engineering. It’s both the balloons and the test drives that make you want to use a new chaos engineering tool.

You can set up recurring game days. You can start your team off with a single event to introduce them to the idea. You can buy some fancy cards for writing down chaos experiment ideas, or you can use sticky notes. Whatever you think will get your team to appreciate the benefits, without feeling like it’s forced upon them, will do. Make them feel they’re not wasting their time. Don’t waste their time.

That’s all I have for the buy-in -- time to dive a level deeper. Let’s see what happens if you apply chaos engineering to a team itself.