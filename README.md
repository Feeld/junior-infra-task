![Feeld Logo](https://i.imgur.com/7MG1EA7.jpg)

# Junior Infrastructure Engineer Recruitment Task

Congratulations on making it through to the penultimate stage of our recruitment process! 

We'd like to get an idea of how you work, left to your own devices, and so I have a task for you. Please read the specification carefully - there's nothing intended to trip you up or catch you by surprise. If you need clarification about any of it, then please drop an email to dave@feeld.co and I'll be happy to help.

This recruitment task differs slightly from our normal process, in that since mentorship is part of the position, that same mentorship is available during the task. You won't lose (or gain) anything in your assessment by asking questions, so while I ask that you don't seek technical help unless you do need it, don't be afraid to ask. The support available will be limited to the more technical aspects of the task - I'm trying to evaluate your work and skillset after all - but feel free to ask, and if it's something too basic, I'll say so and you won't be penalised. Send any requests to dave@feeld.co and I'll get back to you as soon as I can.

## Task: Solution Evaluation

One thing we commonly do in infrastructure land is to evaluate options of a particular class of software or service, decide on one, then deploy and support it.

I'd like you to evaluate options for a monitoring system, both self-hosted and Software-as-a-Service (SaaS) offerings.

Our platform is built around Kubernetes on Google Cloud Platform, and your evaluation should consider the strength, ease, and reliability of each option's integration with Kubernetes and containerised compute in general, along with Google Cloud Platform APIs. Other systems we will need to integrate with, and should be included in your analysis, include Postgres, Redis, RabbitMQ, and MongoDB.

You are encouraged to find additional software and services to evaluate, but at a minimum your evaluation should include the following -

**Self-hosted**

- Icinga
- Zabbix
- Prometheus

**SaaS**

- New Relic
- Google Cloud Stackdriver
- OpsGenie

Please write a report detailing your evaluation of each, and finally include a recommendation (ideally of a single option, but of no more than two options) along with the reasoning for your selection(s). You will not be penalised based on how many options you finally recommend, as long as it does not exceed two options.

Please format your report using [GitHub Markdown](https://guides.github.com/features/mastering-markdown/).

### Time expectations

Your submission will be expected **one week** after it is assigned. This should give you plenty of freedom to fit it around your existing commitments. If for some reason you think you will need longer, reasonable requests for more time (sent to dave@feeld.co) will not be penalised **if submitted within the first two days**. 

### Submission process

Fork this repository, **commit your work as you go**, and send a pull request when your report is complete. Any images or other rich media can be committed to the repository alongside your report.

It is **very important** that you commit as you go rather than just committing once at the end, as I'd like to see the relative timestamps of your progress once you're done. Don't worry about sending a message with your timestamps, as you may be fitting this task around existing employment or other commitments. Just **commit as you go**.

### Bonus points

> These are entirely optional further objectives which you should only pursue if you actively want to. By attempting and/or delivering them, you can only increase your score, not decrease it.

* Write Kubernetes manifests to deploy the highest-scoring self-hosted option you evaluate. Use [minikube](https://minikube.sigs.k8s.io/) to develop your manifests. Write them as plain YAML, don't use Helm.
* Configure web and TLS certificate monitoring for the Feeld website at https://feeld.co using one of the options you evaluate. Document the configuration process with screenshots if you use a SaaS to do this, otherwise commit the configuration files to this repo.
* Give a list of checks you would set up, given the requirement to monitor our HTTP API, Postgres, Redis, RabbitMQ, and MongoDB. You don't need to set them up, just list them.

## Key Points

I'd like to reiterate that there are no traps or trick questions involved here. If anything is unclear, or you need some technical points explained, email dave@feeld.co and I'll assist.

To sum up

* Please deliver your work as a pull request no later than **one week** after you receive this assignment.
  * Requests for more time (including reasoning) will not be penalised during the **first two days** of the assignment.
* Commit your work **as you progress** rather than just once at the end. **Pushing** during the task period is optional, the important thing is that the final submission has a commit history.
* If you have any questions, email dave@feeld.co



