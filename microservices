# Microservices

## What is
Microservices are smaller in size and scope, but their use introduces more moving parts in an application, especially because microservices are distributed and running independently of each other in their own distributed containers. This introduces a high degree of coordination and more opportunities for failure points in the application.

## Development principles w.r.t DevOps
- Self-contained, Independently deployable
- be Configurable
- be Transparent
- Communicative

## Building the 12factor microservice application
Heroku’s Twelve- Factor Application manifesto (https://12factor.net/).

**Codebase**—All application code and server provisioning information should be in ver- sion control. Each microservice should have its own independent code repository within the source control systems.

**Dependencies**—Explicitly declare the dependencies your application uses through build tools such as Maven (Java). Third-party JAR dependence should be declared using their specific version numbers. This allows your microservice to always be built using the same version of libraries.

**Config**—Store your application configuration (especially your environment-specific configuration) independently from your code. Your application configuration should never be in the same repository as your source code.

**Backing services**—Your microservice will often communicate over a network to a data- base or messaging system. When it does, you should ensure that at any time, you can swap out your implementation of the database from an inhouse managed service to a third-party service. 

**Build, release, run**—Keep your build, release, and run pieces of deploying your application completely separate. Once code is built, the developer should never make changes to the code at runtime. Any changes need to go back to the build process and be redeployed. A built service is immutable and cannot be changed.

**Processes**—Your microservices should always be stateless. They can be killed and replaced at any time without the fear that a loss-of-a-service instance will result in data loss.

**Port binding**—A microservice is completely self-contained with the runtime engine for the service packaged in the service executable. You should run the service without the need for a separated web or application server. The service should start by itself on the command line and be accessed immediately through an exposed HTTP port.

**Concurrency**—When you need to scale, don’t rely on a threading model within a single service. Instead, launch more microservice instances and scale out horizontally. This doesn’t preclude using threading within your microservice, but don’t rely on it as your sole mechanism for scaling. Scale out, not up.

**Disposability**—Microservices are disposable and can be started and stopped on demand. Startup time should be minimized and processes should shut down grace- fully when they receive a kill signal from the operating system.

**Dev/prod parity**—Minimize the gaps that exist between all of the environments in which the service runs (including the developer’s desktop). A developer should use the same infrastructure locally for the service development in which the actual service will run. It also means that the amount of time that a service is deployed between environments should be hours, not weeks. As soon as code is committed, it should be tested and then promoted as quickly as possible from Dev all the way to Prod.

**Logs**—Logs are a stream of events. As logs are written out, they should be stream- able to tools, such as Splunk (http://splunk.com) or Fluentd (http://fluentd.org), that will collate the logs and write them to a central location. The microservice should never be concerned about the mechanics of how this happens and the developer should visually look at the logs via STDOUT as they’re being written out.

**Admin processes**—Developers will often have to do administrative tasks against their services (data migration or conversion). These tasks should never be ad hoc and instead should be done via scripts that are managed and maintained through the source code repository. These scripts should be repeatable and non-changing (the script code isn’t modified for each environment) across each environment they’re run against.
