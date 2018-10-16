Hi! My name is [Michael](https://mhausenblas.info) and I'm a developer advocate and cloud native [ambassador](https://www.cncf.io/people/ambassadors/). Here, I share some thoughts and considerations around using cloud native technologies, including Kubernetes, observability tools such as Prometheus, service meshes,  and serverless offerings.

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

- All of our source code is in a version control system such as Git, Mercurial, svn or whatnot.
- We know about container (base) image hygiene such as footprint, build vs runtime environment, attack surface, etc.  
- We have a CI/CD pipeline and know how to use it.
- We have a (private, secure) container registry and know how to use it.
- Our developers have either local Kubernetes environments or access to dedicated namespaces for day-to-day development.
- Our dev and ops folks have a 360 view on apps and infra, we use observability tooling everywhere.

Checked all items off the list? Pinky promise? 

Cool, you're ready …

So, what's next? Well, think about what kind of app you're doing. Is it a lift and shift of an existing app? Breaking down a monolith into a bunch of microservices? Are you writing a native app from scratch? Here are some rough guidelines and indicators for each case:

- You have a _commercially available off-the-shelf_ (COTS) app such as WordPress, Rocket Chat or whatever and you want to run it on Kubernetes. The app itself is not "aware" it runs on Kubernetes and usually doesn't have to be. Kubernetes controls the app's life cycle, that is, find node to run, pull the container image, launch container(s), carry out health checks, mount volumes, etc, and that is that. You benefit from Kubernetes as a runtime environment and that's fine.
- You write a bespoke app, something from scratch (with or without having had Kubernetes as the runtime environment in mind) or an existing monolith you carve up into microservice. You want to run it on Kubernetes. It's roughly the same modus operandi as in case of the COTS app above with a twist:
  - 
- The case of a _cloud native_ or _Kubernetes native_ application that is fully aware it is running on Kubernetes and leverages Kubernetes APIs and resources to some extent.

### Good practices

So, let's face it, there are [no best practices](https://www.forbes.com/sites/mikemyatt/2012/08/15/best-practices-arent/#6837047e407b), but over time the community documents and collects things that can maybe be called "good practice". As in: worked for me, in my setting but YMMV.

Now, here are some pointers to good practice and/or collection of such, to get you started:

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

It's simple. Install it, use it together with Grafana. Also, if you're looking for retaining your metrics in the long term, [there are options](https://github.com/mhausenblas/docs/blob/master/content/blog/2018-09-03-lts-options.md) (@@TODO: update dat link when blog post goes live).

## Let's talk about service meshes

A word on maturity: we're, at time of writing this in end of 2018, with service meshes where we were between 2015 and 2017 with container orchestrators. Remember to "container orchestration wars"? We had Swarm, Mesos/Marathon and then Kubernetes came along (honorable mention: Nomad, which I very much like, just a little late to the party). It became apparent for folks that it's prolly a good idea to use a container orchestrator but it was unclear which one to pick since there was no clear winner. So folks often ended up doing home-grown combos of bash scripts and using Puppet, Chef, or Ansible to orchestrate containers. Well, with end of 2017, Kubernetes established itself as the industry standard in this realm and the discussions are nowadays kinda moot.

Again, we're early days concerning service meshes. But, if you have a non-trivial number of microservices (10? 20? 30?) and you find yourself rolling your own solution to manage observability, shape traffic, intra-service or intra-cluster mutual TLS, etc. then maybe, just maybe you're in the right place to consider a service mesh. Here are some options (in order of popularity/community size):

- [Istio](https://istio.io/): the 500 pound gorilla. Everyone seems to do it and back it. Also, make sure to [evaluate](https://tech.bigbasket.com/bigbaskets-experience-with-istio/) it carefully. 
- [Linkerd2](https://linkerd.io/2/overview/): a nice and lightweight alternative, I took a closer look at it [here](https://hackernoon.com/linkerd-2-0-service-ops-for-you-and-me-281cc5bd6424).
- [Consul Connect](https://www.hashicorp.com/blog/consul-1-2-service-mesh): can't say much since I haven't tried it but looks promising to me.

## Let's talk about serverless

Where? In the public cloud such as AWS Lambda or Azure Functions or [on top of Kubernetes](https://go-talks.appspot.com/github.com/mhausenblas/2018-state-of-faas-on-kube/main.slide)?

More to come …