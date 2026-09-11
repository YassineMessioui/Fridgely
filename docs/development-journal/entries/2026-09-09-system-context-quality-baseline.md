# 2026-09-09 — System context and quality baseline

## Context

After creating [Epic #49: Architecture Foundation](https://github.com/YassineMessioui/Fridgely/issues/49), the first task was to understand the environment Fridgely must operate in before comparing application frameworks, databases, or hosting vendors. The discussion focused on product intent, users, capacity, privacy, performance, external dependencies, operations, and learning goals.

This session produced decision inputs rather than a technology selection. The detailed baseline is tracked in [Issue #50](https://github.com/YassineMessioui/Fridgely/issues/50).

## Goal

Turn the MVP requirements and product-owner preferences into concrete constraints and measurable quality targets that can be used to evaluate future architectural options.

## Decisions and tradeoffs

| Decision | Why | Alternatives considered | Consequences |
| --- | --- | --- | --- |
| Balance delivery with learning | A working portfolio MVP matters, but the project is also intended to expose unfamiliar technologies and system-design techniques | Optimize only for delivery speed or only for experimentation | Technology comparisons become part of feature planning, while selected tools must still support a stable MVP |
| Target a small invited global audience | The deployed application should be usable by others without adopting commercial-scale requirements | Personal-only application or unrestricted public launch | The MVP needs real security and reliability baselines but can avoid multi-region and high-scale complexity |
| Design for at least 100 accounts and about 10 simultaneously active users | Registered-user storage and concurrent workload are different capacity concerns | Treat 100 users as concurrent or avoid a measurable target | Early performance validation can use a realistic workload without premature scaling work |
| Prioritize performance, usability, and low cost | These qualities most directly support the intended portfolio experience and inventory hypothesis | Make scalability or maximum delivery speed the top priority | The architecture must stay responsive and affordable; security, privacy, reliability, accessibility, and maintainability remain mandatory baselines |
| Build mobile-first responsive web | Inventory entry is expected to happen mainly from a phone, while web is the most approachable MVP delivery channel | Native mobile first or desktop-first web | Touch ergonomics and small-screen flows guide the UI, while native capabilities remain deferred |
| Accept refresh-based consistency initially | Real-time synchronization would add infrastructure and state-management complexity before the hypothesis is validated | Real-time streaming or offline-first synchronization | Multiple devices are supported, but users may need to refresh to see changes made elsewhere |
| Use managed services where they reduce operational burden | The project should focus on learning architectural tradeoffs without requiring every infrastructure component to be operated manually | Fully self-managed infrastructure | Provider responsibilities and vendor dependence must be understood and documented |
| Use local, staging, and production environments | Merged work should be validated before an intentional release | Local and production only, or a preview environment for every pull request | Merges deploy to staging; production release remains a manual decision |
| Allow essential authentication email only | Email verification and password recovery may be necessary for secure email-based accounts | No email at all or broader notification features | The authentication design may include transactional email, while product notifications remain outside the MVP |
| Delete primary account data immediately and expire backup copies within 30 days | Users need meaningful deletion without requiring impossible instantaneous removal from every backup | Permanent retention or immediate physical deletion from all backups | Storage and backup providers must support a documented deletion and retention path |
| Store analytics within Fridgely as the initial preference | The product owner prefers not to introduce a separate analytics provider without need | Third-party analytics platform | Analytics must be isolated so collection failures never block core product behavior; the assumption still requires technical validation |
| Apply accessibility fundamentals without formal certification | Core flows should avoid obvious barriers even though a certification program would expand MVP scope | Ignore accessibility or commit to a formal WCAG audit | Semantic markup, labels, keyboard access, focus visibility, contrast, and clear validation become engineering expectations |

## Provisional system context

Fridgely serves visitors evaluating the public project, registered home cooks managing private data, and the product owner reviewing architecture and releases. The application owns the web experience, application logic, inventory and shopping data, the initial recipe dataset, and product analytics.

Potential external dependencies include managed hosting, managed persistent storage, authentication and transactional email, and a possible low-cost recipe API. These are system relationships, not vendor decisions.

## Quality baseline

- Main pages should load within two seconds on a good consumer Wi-Fi reference connection under normal MVP usage.
- Common inventory actions should be completable in under ten seconds.
- The system should support at least 100 registered accounts and approximately 10 simultaneously active users.
- Acknowledged inventory changes should persist without normal data loss.
- Recipe or analytics failures must not prevent inventory and shopping-list use.
- Normal operation should preferably use free tiers and remain within approximately €10–€30 per month when paid services are justified.
- Core flows should complete without known blocking errors and should provide understandable failure states.

## Deferred opportunities

- Real-time multi-device synchronization
- Offline support
- Barcode or QR scanning
- Searchable food catalog
- Search-engine optimization
- Formal accessibility certification
- Multi-region deployment

## Work completed

- Created and linked [Issue #50](https://github.com/YassineMessioui/Fridgely/issues/50) beneath the Architecture Foundation epic.
- Added the issue to the Sprint Board and moved it into active work.
- Propagated relevant confirmed constraints to the performance, security, authentication, responsive-web, analytics, and MVP-validation issues.
- Added a clearly labeled recipe-source assumption to the recipe-data-source issue without selecting a provider.

## Challenges and changes in direction

- “Without any errors” could not be treated as an absolute engineering guarantee. It was reframed as having no known blocking errors in core journeys and providing graceful failure states.
- Registered accounts and active concurrency were initially discussed as one scale target. They were separated into at least 100 stored accounts and approximately 10 simultaneous active users.
- A deployment after merge is a staging deployment rather than a pull-request preview. The agreed path is therefore local development, staging after merge, and manual production release.
- Accessibility terminology was unfamiliar, so the MVP commitment was translated into concrete interface practices rather than a formal certification target.

## Validation

- The product owner explicitly confirmed the capacity, deletion, environment, transactional-email, and accessibility baselines.
- GitHub confirms that Issue #50 is linked beneath Epic #49 and is tracked on the project board.
- Relevant existing issues now link back to the architecture baseline.

The performance and capacity targets have not yet been load-tested, and no technology vendor has been selected.

## Lessons

- Capacity needs separate measures for stored users and concurrent activity.
- Quality attributes become useful when expressed as observable scenarios rather than words such as “fast” or “stable.”
- System context identifies relationships before vendors, keeping technology evaluation grounded in responsibilities.
- Deferred capabilities should remain visible without shaping the MVP architecture prematurely.
- An unfamiliar standard can often be converted into a small set of concrete engineering behaviors before deciding whether formal compliance is necessary.

## Open questions

- Can one deployment region provide an acceptable experience for the initial global audience?
- Should the initial recipe source be a Fridgely-managed dataset or a low-cost external API?
- Is storing product analytics inside the application database operationally appropriate?
- Which managed services can meet the deletion and backup-retention expectation?
- Which application shape best satisfies these constraints while maximizing learning value?

## Next steps

- Produce and review the repository system-context diagram and quality-attribute scenarios for Issue #50.
- Compare a full-stack modular monolith with separated frontend and backend applications.
- Record accepted architecture decisions as ADRs before beginning the first inventory implementation slice.
