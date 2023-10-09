# How We Work

This document is the full outline of how CSG does its work.

We adopt two philosophies: [Scrum](https://scrumguides.org/scrum-guide.html) and [Shape Up](https://basecamp.com/shapeup). You will see both of them utilized here.

## The Work Loop

Our work loop is simple:

1. Define the work with the guest (Week 1)
2. Do the work (Week 2, known as [the sprint](https://scrumguides.org/scrum-guide.html#the-sprint))
3. Review the work with the guest (Week 3)
4. Return to step 1.

Tenant 1: **We fail as fast as possible**

We seek to, in step 3, find our failures. We then redefine our product based on these failures. Without looking for our small-ish failures every week, we'll be even more distraught when we encounter our large failures at the end of the project.

## The Sprint Meeting

The sprint meeting is a 50 minute [timeboxed](https://en.wikipedia.org/wiki/Timeboxing) meeting that has 3 steps.

1. Sprint Review (demos)
2. Sprint Retrospective (meta)
3. Sprint Planning (next)

### 1 - The Review

Reviewing our work as a team is the most important thing before we show a customer. Once the entire team knows what happened last sprint, they are empowered to take the helm and work on the same project next sprint. This is only possible in a team less than ~12 people.

Tenant 2: **Small teams eat large teams for breakfast**

### 2 - The Retrospective

Sometimes we do work poorly. Sometimes people don't have the tools they need. Sometimes, midterms are coming up and we can't all finish our tasks. We need to know these things. Retrospective is the time that everyone begins by:

1. Talking about the things that went poorly this sprint
2. Talking about the things that went great this sprint

Tenant 3: **Speak of the bad before the good**

### 3 - The Planning

Now that we know what was good for the team, we can begin planning the next sprint. This is a fairly in-the-weeds process.

1. Assign each story to 2 people
2. Make sure everyone knows why they are doing their work

Tenant 4: **Nothing good happens without at least 2 people**

### Summary

Now that we know about the basic tenants of the sprint meeting, let's talk about how work is *defined*

## Finding The Next Thing

To be in CSG, you must be an innovator. You must understand what the next problem is. You must talk to the guest and understand what to do next. You must *find the next thing*. We have 2 tools that empower us to *document this next thing*.

### Basecamp

Basecamp contains a lot of the way that execs do work.

#### The Todo List

The todo list contains two things:

1. The operational list (things that are one-off tasks that do not produce an artifact)
2. The booper list (booper setups!)

#### The Icebox

This is where all the unshaped/shaped work goes that we are not ready to do yet. 

Sometimes, your project won't be one of the lists in here. In that case, create a new list inside of here for your project.

Otherwise, just add the todo in a *story format*.

#### The Project Board

The project board is where **all work originates** for *developers*

Much of this board is a merging between the Scrum and Shape Up philosophy.

Everything here should be laid out in a "As __ I want __ so I can __." This is so that at a glance, we have: the guest, the task, and why we're doing it.

It has a few parts that I will explain here.

##### Unshaped work

Unshaped work is work that is *rough* only. It has no solution, it is merely an idea that has no form.

The process of shaping is what takes something from the unshaped column to the shaped column. This is *not* creating a new card, but editing the old one and adding more details as shown in the step below.

##### Shaped work

[Shaped work](https://basecamp.com/shapeup/1.1-chapter-02) is work that is:

1. Rough
2. Solved
3. Bounded

Wireframes are too concrete. Words are too abstract.

<ins>Rough</ins>

All work must be rough. This is *usually* only applicable to UI changes. This should be a **sketch** of the thing that the guest want to have done. It is intentionally without detail.

<ins>Solved</ins>

All work must be solved. This is applicable to *all* tasks. You must have a clear path forward and a full understanding of exactly what the customer wants. This is where you will spend most of your documentation time.

<ins>Bounded</ins>

All work must be bounded. Developers *love* to make things. They love to come up with creative solutions. You must keep them within the bounds of the story so that they do not do something that they do not have to do. Developers experience burnout whenever the bounds are not clearly defined.

Bounded means that you have thought through and documented everything that a developer *might* want to do extra and telling them not to do it.

<ins>Summary</ins>

This work may or may not be queued next sprint. The only requirement to be in this column is that it is *shaped* work.

##### Queue

The queue is work that is going to be inserted into the next sprint. It is dragged into [In Progress](#in-progress) whenever the next sprint starts.

##### In Progress

This is work that is in the current sprint and is being worked on.

Everything in here should take *one week* and one week **only**. Otherwise, it must be broken down further.

Whenever something is done here, it should go into [In Review](#in-review).

If it fails, it should be [punted](#punt).

##### Punt

This is work that was not finished this sprint and must be sent back.

##### In Review

This is where you review the artifact produced by the story with the guest. You should schedule a meeting with the guest *directly* after the sprint meeting. Review must be done within the week so that you may redefine the work for the next iteration.

This is timeboxed to a *15 minute* meeting.

Once this is finished, it may be dragged into *done*!

Make sure that you make stories in [Unshaped Work](#unshaped-work) after this meeting that defines the changes that the customer wants.