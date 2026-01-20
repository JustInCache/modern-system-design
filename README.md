# Modern System Design

A curated collection of modern system design architectures and trade-offs for real-world applications. This repo documents classic architecture patterns (monoliths, microservices, serverless, event-driven) and provides deep dives into popular products.

## Architecture Patterns

- **Monolithic**: Single deployable unit, simple to start, harder to scale across teams.
- **Microservices**: Independent services, scalable and team-aligned, higher operational overhead.
- **Serverless**: Event-driven, auto-scaling, pay-per-use, vendor constraints and cold starts.
- **Event-Driven**: Asynchronous communication, high decoupling, requires strong observability.
- **Layered / N-tier**: Clear separation of concerns, widely used in enterprise systems.
- **CQRS + Event Sourcing**: Separate reads/writes, auditability, more complex data flows.

## Application Deep Dives

Each document below will include requirements, scale assumptions, architecture diagrams, data model, critical flows, and trade-offs.

- [Uber System Design](docs/uber.md)
- [Spotify System Design](docs/spotify.md)
- [Netflix System Design](docs/netflix.md)

## Contributing

Feel free to propose new applications or improvements via issues or pull requests.
