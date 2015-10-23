---
layout: post
title: "the one (clear) advantage of o.r.m."
description: ""
category: 
tags: []
---
{% include JB/setup %}

As someone who started building web applications before object-relational
mapping became widespread in all frameworks, I sometimes find it harder
to get an application going with some of these modern frameworks. From recent
experience, I'm not the only one.

I think there are some benefits to O.R.M., particularly for the plethora
of younger developers who have not been formally introduced to relational
databases and are only familiar with "objects".

But one clear benefit of O.R.M. is that
any of the major frameworks allow you to switch database technologies without
touching your code--except for the settings file, and there are even ways of
specifying the settings that allow for these changes. I don't think people
change database management systems within the life of a product that often
but it does happen from time to time. A more common occurrence is using
different DBMSes in different environments, like development, testing, and
production.

It's not uncommon to use a Derby or SQLite DBMS in development but deploy
to an Oracle or PostgreSQL one. But for apps that only need SQLite, say, I
don't think anything is gained from using O.R.M. while losing the flexibility
of writing code the way you want and, in particular, defining and manipulating
data the way you see fit.

I would say the best way to approach the decision of which framework, if any,
you will use is from the point of view of your data model. If your data model
is relational, then it's hard not to see that the best approach to use is the
relational one. Same goes for a graph or network model or some other data
model.

I just think that the O.R.M. way has been thrust on a lot of us and we've been
forced to adjust. Many people probably felt that way with the relational model
and there have been many debates with Chris Date about this. I, for one, would
still like to write some SQL from time to time.