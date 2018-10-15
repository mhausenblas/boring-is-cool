Hi! My name is [Michael](https://mhausenblas.info) and I'm a developer advocate and cloud native [ambassador](https://www.cncf.io/people/ambassadors/). Here, I share some thoughts and considerations around using cloud native technologies, including Kubernetes, observability tools such as Prometheus, and serverless offerings.

1. [Why?](#why)
1. [Kubernetes](#lets-talk-about-kubernetes)
1. [Prometheus](#lets-talk-about-prometheus)
1. [Service meshes](#lets-talk-about-service-meshes)
1. [Serverless](#lets-talk-about-serverless)

----

## Why?

### Why you would want to read this

You have heard about cloud native [technologies](https://landscape.cncf.io/) and [success](https://kubernetes.io/case-studies/) [stories](https://serverless.com/learn/use-cases/). You wonder where and how to start and get the most out of it. Congrats! You're exactly right here.

### Why I am writing this

A fair part of my work consists of being [on the road](http://mhausenblas.info/on-the-road.html), talking with folks at events, with customers on-site, meeting up with partners to understand their offerings, helping on StackOverflow and on various Slack channels. I learn something every time when I'm having these discussions and even more when someone asks me how to do something or why things are like they are. This is my attempt to share some of this knowledge, to give back to the community. Also, I wanted to have a place on the Internetz I can point people to. Talking about human scalability, ha!

## Let's talk about Kubernetes

So you want to benefit from [Kubernetes](https://kubernetes.io/), right? You want portable applications, getting features out to your customers faster, use modern deployment mechanisms, have autoscaling, and more? 

I've got good news and not so good news for you. Yes, it's totally feasible, but you gotta do your homework first. You have to first do the, surprise, boring stuff (!)

Let me walk you through it …

### Begin at the beginning

> "Begin at the beginning," the King said, very gravely, "and go on till you come to the end: then stop.”

&mdash;&mdash; [Lewis Carroll, Alice in Wonderland](https://www.goodreads.com/quotes/6305-begin-at-the-beginning-the-king-said-very-gravely-and)

So, what *is* the beginning? It starts with your team and your wider organization. Like, everyone. This is the hard part and unfortunately the technologies available can't help you there. Make sure that [developers and folks with ops roles are incentivized](https://www.usenix.org/conference/lisa16/conference-program/presentation/eckhardt) in the same direction. Go for lunch together. Talk. [Whatever it takes](https://basecamp.com/books/calm), make sure you're on the same page for what is coming. Do it now, I'll wait here …

OK. You ready?

Let's get to the "easy" stuff, the tech. Here's a little checklist, in this order:

- [ ] All of our source code is in a version control system such as Git, Mercurial, svn or whatnot.
- [ ] We know about container (base) image hygiene such as footprint, build vs runtime environment, attack surface, etc.  
- [ ] We have a CI/CD pipeline and know how to use it.
- [ ] We have a (private, secure) container registry and know how to use it.
- [ ] Our developers have either local Kubernetes environments or access to dedicated namespaces for day-to-day development.
- [ ] Our dev and ops folks have a 360 view on apps and infra, we use observability tooling everywhere.

All checked off? Cool, we're ready.

### Good practices

Some pointers to get you started:

1. Install:
  - [Kubernetes the hard way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
  - [Managing Kubernetes](http://shop.oreilly.com/product/0636920146667.do)
1. Development:
  - [Developing on Kubernetes](https://kubernetes.io/blog/2018/05/01/developing-on-kubernetes/)
  - [Apps life cycle](http://shop.oreilly.com/product/0636920175131.do)
  - [Troubleshooting apps](http://troubleshooting.kubernetes.sh)
1. Functional areas: 
  - [Stateful Apps](http://stateful.kubernetes.sh)
  - [Network](https://mhausenblas.info/cn-ref)

## Let's talk about Prometheus

## Let's talk about service meshes

## Let's talk about serverless
