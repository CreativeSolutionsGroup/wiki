# How We Work

This document is the full outline of how CSG does its work.

We adopt two philosophies: [Scrum](https://scrumguides.org/scrum-guide.html) and [Shape Up](https://basecamp.com/shapeup). You will see both of them utilized here.

Before you decide to switch these processes, realize that the choice for these philosophies was made with much care. 

1. We chose Scrum because we needed faster iteration times than Shape Up with regular team retrospectives.
2. We chose Shape Up because we needed to shape our work better.

With a comination of both 1 and 2, we have seen the productivity of a *part-time* team increase immensely. While one or the other may be better for a full-time team, we have found a healthy medium here.

## The Tenants

Tenant 1: **We fail as fast as possible**
Tenant 2: **Small teams eat large teams for breakfast**
Tenant 3: **Speak of the bad before the good**
Tenant 4: **Nothing good happens without at least 2 people**
Tenant 5: **All work must have an external guest that will be benefitted.**

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
3. Realize that we do *not* score [stories](./WhyWeDontScore.md).

Tenant 4: **Nothing good happens without at least 2 people**

### Summary

Now that we know about the basic tenants of the sprint meeting, let's talk about how work is *defined*

## Finding The Next Thing

To be in CSG, you must be an innovator. You must understand what the next problem is. You must talk to the guest and understand what to do next. You must *find the next thing*. We have 2 tools that empower us to *document this next thing*.

### Basecamp

Basecamp contains a lot of the way that execs do work.

#### The Todo List

The todo list contains two things:

1. The operational board (things that are one-off tasks that do not produce an artifact)
2. The booper board (booper setups!)

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

Tenant 5: **All work must have an external guest that will be benefitted.**

This is where you review the artifact produced by the story with the guest. You should schedule a meeting with the guest *directly* after the sprint meeting. Review must be done within the week so that you may redefine the work for the next iteration.

This is timeboxed to a *15 minute* meeting.

Once this is finished, it may be dragged into *done*!

Make sure that you make stories in [Unshaped Work](#unshaped-work) after this meeting that defines the changes that the customer wants.

### GitHub

Github has two purposes.

1. Store the code
2. Provide documentation for developers

The code storage is provided through repositories. That is not important for this document.

#### Documentation for Developers

Documentation for developers is provided using the [Kanban Board](https://github.com/orgs/CreativeSolutionsGroup/projects/9). This is where the [Developer Backlog](https://scrumguides.org/scrum-guide.html#sprint-backlog) exists.

This is a traditional kanban board that goes through all the steps of work for developers. It is *not* a story board. It is a *task* board. It is much lower level than stories. If there is a "director" position on CSG currently, they will likely only work with the [Project Board](#the-project-board) and not this board.

##### Todo

These are tasks that are in the sprint but have yet to be started.

##### In Progress

These are tasks that are currently being worked on by developers.

##### Punt

These are tasks that need to be sent to the next sprint. It is very similar to the [Punt](#punt) of the Project Board.

##### In Review

This is where the technical execs are able to review the work of the developers. Technically, everyone should be able to do reviews, but currently it is relegated to technical execs.

##### Done

These are *closed* issues that are complete.