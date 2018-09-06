
# What is Cloudspin?

Cloudspin is a collection of code I (Kief Morris) am using on to explore ways to structure and manage infrastructure as code projects. I am using it to help illustrate concepts, patterns, and practices from my book, [Infrastructure as Code](http://infrastructure-as-code.com/book/), articles, and workshops. I am also using it with client teams I work with at [ThoughtWorks](https://thoughtworks.com) to work out ideas for project structures and tooling.

I'd like to see this evolve into a community-driven set of tools and template projects (replacing "I" with "we" in this documentation!) For the moment, I'm making fairly radical changes on an unpredictable basis (in flurries of activity), so it's likely to be inconsistent and even broken at times.

Feel free to copy and use material from here (subject to the terms of the MIT license), but you will need to modify and extend it to make it useful for your own project.


## Why Cloudspin?

Currently, most people and teams managing infrastructure with tools such as Terraform, CloudFormation, etc. define their own unique project structures, and write their own unique wrapper scripts (using make, shell, rake, or whatever) to run that tool and associated tasks. Essentially, each project is a special snowflake.

The goal for cloudspin is to evolve a common structure and build tooling for infrastructure projects, focused on the lifecycle of "[stacks](http://infrastructure-as-code.com/patterns/2018/03/28/defining-stacks.html)" - groups of infrastructure elements provisioned on dynamic infrastructure such as IaaS clouds.

The hypothesis is that, with a common project structure and tooling, teams can:

- Spend less time creating and maintaining scaffolding, and more time on higher value work,
- Bring new team members up to speed more quickly,
- Rapidly create new infrastructure projects, and add new infrastructure to existing projects,
- More easily debug and improve infrastructure,
- Adopt mature engineering practices such as TDD and CD for their infrastructure,
- Have more fully featured infrastructure sooner in a project.

Additionally, common conventions and structures for infrastructure projects can foster an ecosystem:

- People can create and share tools and scripts that work with the common structure, creating an ecosystem,
- People can then create and share infrastructure code for running various software and services, creating a community library.


## Philosophy

- [Convention over configuration](https://en.wikipedia.org/wiki/Convention_over_configuration).
-- The tool should discover elements of the project based on folder structure
-- A given configuration value should be set in a single place
-- Implies a highly "[opinionated](https://medium.com/@stueccles/the-rise-of-opinionated-software-ca1ba0140d5b)" approach
- Encourage good agile engineering practices for the infrastructure code
-- Writing and running tests should be a natural thing
-- Building and using [infrastructure pipelines](http://infrastructure-as-code.com/book/2017/08/02/environment-pipeline.html) should be a natural thing
-- Secure by default
- Support evolutionary architecture
-- Loose coupling of infrastructure elements
- Empower developers / users of infrastructure


## What is in Cloudspin

At the moment, cloudspin includes:

- The [cloudspin-stack](https://github.com/cloudspinners/cloudspin-stack) Ruby library, which provides classes for interacting with stack definitions (source code) and instances. This is currently implemented for Terraform projects, for AWS. Other cloud providers should be easy enough to implement. In theory it can be adapted to use tools other than Terraform (e.g. CloudFormation), but in practice it'll probably need a fair bit of work.
- Some conventions for structuring project folders for infrastructure stacks, for configuring and provisioning infrastructure stack instances, for packaging infrastructure (Terraform) code into an artefact, and using it in a delivery pipeline (currently with AWS CodePipeline).
- A command-line tool (included in the cloudspin-stack gem), and some [rake tasks](https://github.com/cloudspinners/cloudspin-stack-rake) which can used to manage stack instances using the cloudspin-stack classes, following the conventions described here.
- An example stack project, [spin-stack-network](https://github.com/cloudspinners/spin-stack-network), using these conventions and tools.

What I'd like to add over time, with the help of a community:
- Conventions and tools for configuring stack instances from different sources (files in the project, key/value stores)
- Conventions and tools for integrating multiple stacks
- Conventions and tools for organizing and managing collections of stacks in environments
- More example projects
- Develop a library of template stack projects that people can share and use
- Provide examples and templates for common core services - CI and CD tools, monitoring, log aggregation, etc.
- Add support and examples for more cloud providers
- Consider how to support additional infrastructure tools beyond Terraform


## This documentation

The purpose of this reference guide is to explain the conventions the cloudspin code are meant to support, and how to use them. It's quite likely to lag the actual code, so fair warning.


