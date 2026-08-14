---
title: "In the last year I learned how to use AI"
---

*Part one of a series on things I have been trying with AI.*

On the first of April this year I paid twenty dollars for a Claude subscription. On the eighth of April I cancelled it.

I only know that because I went digging through my email last week. The cancellation notice is still sitting in my inbox, politely telling me my access would expire on the first of May and that I could re-subscribe at any time. Three weeks later I did exactly that, and by the eighteenth of July I had moved to the hundred dollar a month plan. Four weeks after that I gave it administrator access to a computer that somebody else was actively controlling, which is a story of its own and the next post in this series.

Seven days to quit and about fifteen weeks to hand over the keys. I have been trying to work out what happened in between, and the honest answer is that I do not remember most of it, because it happened gradually enough that I never noticed it happening.

## This was not a first attempt

The part that makes the cancellation embarrassing rather than reasonable is that I was not new to any of this.

I started using AI to write code in early 2023, inside ChatGPT, and what I used it for then was almost nothing. Configuration files. A regex I could not be bothered to think through. Small snippets I would have found on Stack Overflow anyway, delivered slightly faster and without the arguing. I was on Anthropic's developer mailing list from at least March 2024, and I have the emails to prove it, announcements about tool use and Claude 3.5 landing in my inbox while I mostly ignored them.

Over the following couple of years the thing quietly got better and I quietly noticed. It went from config files to being able to produce a working web page. Then to a basic app that mostly held together. Every few months the ceiling moved and I would test it again, get a bit more out of it than last time, and go back to writing things myself for anything that actually mattered.

That is the mode I was in when I subscribed in April. I was using a much better tool in exactly the way I had used a much worse one, which is that I would think of a small self-contained thing, ask for it, paste the answer in, and carry on.

Then that week I was travelling and busy with other work, and I barely opened it. That is the actual reason I cancelled, and it is a duller reason than the one I would like to give you. There was no verdict, no moment of concluding it could not do what I needed. I saw a twenty dollar charge for something I had used twice and cancelled it the way anybody cancels a subscription they are not using.

What I could not have told you at the time is that I was never going to use it much, because the only jobs I ever gave it were the ones small enough that I did not really need help with them.

## Watching somebody else do it properly

The thing that actually changed my mind was not a model release. It was a friend.

I met Shubhodeep at Antler last year, and he has been using this stuff far more aggressively than I was. Not for snippets. For building whole things, and for learning subjects he did not previously know. Watching somebody you know work that way is very different from reading about it, because you cannot dismiss it as marketing and you cannot tell yourself they had some setup you do not have. He had the same tools I had. He was getting a completely different return on them.

I do not think he was trying to convince me of anything. He was just doing it in front of me, repeatedly, and after enough of that it stops being possible to believe that the tool is the limiting factor.

So I resubscribed at the end of April and started using it differently. Not more. Differently.

## What differently turned out to mean

If I try to name what actually changed, almost none of it is about writing better prompts, which is the thing everybody talks about.

The first change was that I stopped handing over problems in small pieces. I started giving it the whole context. The repository, the constraints, what I had already tried, what the business actually needs, what the customer complained about. It turns out most of the disappointing results I had been getting were not the model being limited, they were me describing a problem so narrowly that no answer could have been useful.

The second was access. I gave it the ability to run things rather than only to suggest them. Read the codebase, run the type checker, query the database, hit the API, look at the actual output rather than my summary of the output. The gap between an assistant that can see your system and one that can only hear you describe it is much larger than I expected.

The third took me longest and I think it is the one people skip. When something is hard to debug, I now build the instrument before I attempt the fix. On my saree image product I built an internal tool for reproducing and A/B testing prompt changes, because I was tired of arguing with myself about whether an output had improved. On the same product I wrote a small tool that pulls a specific customer's generation history and images into one place, so that when somebody complains I am looking at what they saw rather than imagining it. Those tools are for me, but they are also for the model, and that second part is new. I am now building things whose main job is to let an AI see clearly.

And the fourth was verification, which stopped being a step at the end and became the actual bottleneck. Writing code is no longer the slow part of my week. Looking at what got written is the slow part. Most of my recent working notes have some version of "checked with the type checker, not opened in the browser" sitting in them, and that is a real debt rather than a throwaway caveat.

## What came out the other side

Between May and now, across four repositories, there are about two hundred and seventy commits. I will spare you most of it, but a few things are worth knowing because they are what convinced me.

My saree visualisation product got the heaviest work. In July alone there were fifty seven commits. The one I keep telling people about is a saree draping engine that was reverse engineered from a tailor's Photoshop action, which is to say somebody's manual craft, watched closely enough to turn into deterministic code. In the same month I built GST invoicing and rebuilt the entire checkout, and all of it landed in a single day. I have worked in companies where that specific piece of work was a quarter and a small team. I am not claiming I built the same thing they would have. I am saying the version I needed took a day and a half, and I would previously have scoped it out of existence rather than attempt it.

Then there is my father's textile unit, where I built a factory management system from scratch. The first real commit landed in June with a hundred and six files and about twenty thousand lines in one go, covering production entry, machines, attendance and payroll. It has been in daily use since, and most of what has happened to it since June has been corrections found by people actually using it, which is the correct way round.

The one I am proudest of is the least visible. Our jacquard looms take a proprietary binary file format, and the software that produces those files is expensive. I spent part of the last few months learning that format directly, converting a design from sixty eight to seventy picks by editing the binary by hand, and then writing the procedure down so it can be done again. That is not a thing I would have attempted alone. Not because it is beyond me, but because the ratio of effort to payoff would have been absurd for one design.

## The part that surprised me most

I have deleted an enormous amount of work this year, and I think that is the real signal rather than any of the building.

I wrote a web application for the loom design workflow. I rewrote it three times. In July I deleted about twelve and a half thousand lines of it, kept a small read only reference copy of the parts worth remembering, and replaced the whole thing with a workflow that operates on the raw files directly. A browser tool I had built for converting picks, thirteen hundred lines, went in the same clear out, because it was corrupting a particular class of design and the model could do the conversion correctly without it.

In the factory app I built the finished stock system and then rebuilt it twice inside a single month, because each version taught me what the actual workflow was.

This is the change that took me a while to see. When code was expensive to produce, the sensible instinct was to protect what you had written. Now that it is cheap, protecting it is the expensive habit. A lot of what I built this year was scaffolding to help me work with a model that could not yet do something directly, and a few months later it could, and the scaffolding became the thing slowing me down. I expect that to keep happening and I have stopped being precious about it.

## Where I got to

By the middle of July I was using it enough that the twenty dollar plan was throttling me, so I moved to the hundred. That felt like a large jump at the time and now looks obviously correct, because the thing I was buying was not more tokens. It was not having to ration.

The far end of the arc, so far, was three days ago, when the office computer at the factory turned out to have been compromised for three days by somebody who had installed a legitimate commercial remote management product on it and pointed it at their own server. I gave Claude an elevated shell on that machine and let it run the investigation. Six hours later we had a minute by minute timeline, the whole thing contained, and a decision to wipe the machine.

I would not have done that in April. Not because it would not have worked, but because I would not have thought of it, and I would not have trusted it enough to try. That is the whole distance covered in this post, and the incident itself is the next one.

## What I would actually say I learned

If somebody asks me what I did in the last year, the truthful answer is that I learned how to use AI. Not what it is, or how it works, or which model is ahead this month. How to use it.

The skill turned out to be almost none of the things I assumed. It is not prompt phrasing. It is being willing to hand over the whole problem instead of a filed down version of it. It is giving something enough access to see your actual system, and being deliberate about that rather than nervous. It is building tools whose purpose is visibility, for you and for the model both. It is checking the work, properly, because that is now the part that limits you. And it is throwing away things you spent real time on, without a fight, when they stop earning their place.

The reason I care about any of this is not speed, although the speed is real. It is that a lot of work which used to be impossible for one person at my scale is now merely difficult. Nobody hires a forensics firm for one office desktop. Nobody pays a developer to reverse engineer a loom file format for a single design. That entire category of small, strange, one off work has quietly become available, and if you run something small, that category is most of your problems.

I still cancelled after seven days, and the reason was completely ordinary. I was travelling, I had other work on, and I had hardly touched it. What I did not understand then was that I was only ever going to reach for it occasionally while the jobs I gave it stayed small enough to do myself, and no amount of using it slightly more would have shown me that.

---

*Next in this series: the office computer that somebody else was administering for three days, and what happened when I gave Claude root on it.*
