> ![NOTE]
> Remainder: This can look quite extensive, that's because it is. So don't beat yourself up or think that you should know everything here.
> Most are vaguely aware of the pieces, while focusing on a couple of them.

## Concepts

### Gateway:
Gateways is a part of the application that provides controlled interactions with the outside world to the services you have setup. You can think of this as a Gate in a Wall, or as a Routing layer, directing which services should service each request.

Gateways can provide/offload a lot of responsibilites from the individual services (though they need not). They also allow for unique capabilites that are hard to do with a monolithic application. Due to this you will see them go by many names indicating what responsibilites they cover: Ingress, Egress, Proxy, Reverse Proxy, Gateway, API Gateway, Load Balancer, ++.

Common Usages:
- Service Routing: Aggregate a set of individually developed services behind a single domain.
- Load Balancing: Split traffic between service instances (when 1 computer is not enough).
- Progressive Delivery: Gradually shift traffic to new versions of services for controlled upgrades.
- TLS Termination: Handles TLS/SSL Certificates, allowing services to not bother with communciation encryption (assumes trusted network)
- Circuit Breaker: Stops trafic from reaching the service instance, allowing for recovery
- Authentication: Stops/redirects unauthenticated trafic from passing through
- Authorization: Stops/redirects unauthorized trafic from passing through

### Services:
Services are a single piece of logic that can be versioned, deployed, updated and swapped.

### Stateless:
Container workloads are stateless by deafult. This means that anything you write to the filesystem from the application is gone once the container shuts down.

### Persistence:
To provide persistence across the containers lifecycle we have 2 options:
  1. Volumes: volumes are slices of a filesystem that gets mounted into the container from the host system, allowing the host to manage the lifecycle of the stored data (for datacenters, this is usually called block storage).
  2. External: Rather than storing data locally, we can send requests over the network and store and retrieve it from some other system.

### Communication:
> ![NOTE]
> Websites JavaScript are executing in the **browser**, not inside the container network. So requests from there needs to be routed through the Gateway (if setup).

Networks are used to define the topology of your application, who can talk to who. By default all containers run on the same network and there is a discovery service embedded, meaning they can reach each other by just using the service name instead of an IP address in service to service communication.

## Further Reading

- [Voting App](https://github.com/dockersamples/example-voting-app): Whole swat of examples for how to define a polyglot application

### Useful Third Party Service
> ![NOTE]
> If the links are lacking, just google/ask your LLM for the name and append compose, ie: `NATS Docker Compose`.

- [Ingress (Traefik Proxy)](https://traefik.io/traefik/): One of the ingresses that can be used for personal or smaller projects
- [SQL Database (PostgreSQL)](https://www.postgresql.org/): Open Source SQL database
  - [Database GUI (pgAdmin)](https://www.pgadmin.org/): Web UI for SQL database administration
- [Message Bus (NATS)](https://nats.io/): Message bus for setting up loosely coupled services communicating over a Publisher/Subscriber channel
- [Object Storage (MinIO)](): Cloud Native Object storage for storing blobs (Binary Large Objects), S3 API compliant (the grandaddy of cloud native storage)
- [Identity and Access Management (Keycloak)](https://www.keycloak.org/): Solution for managing users (Identities) and attributes, along with Access Policies and policy decision. Other parts still needs to enforce policies.
