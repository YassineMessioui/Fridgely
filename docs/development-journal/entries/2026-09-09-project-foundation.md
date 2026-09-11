# 2026-09-09 — Project foundation

## Context

Fridgely previously contained an implementation that had selected technologies and generated application code before the desired learning process was established. The project was restarted so its architecture could be designed deliberately, one feature at a time, with the product owner making and understanding each important technology choice.

The existing GitHub repository was deleted through GitHub's web interface and recreated as a public repository with the same name. The local `Fridgely` directory was empty and was initialized as its own Git repository, preventing Git from accidentally treating a parent directory as the project root.

## Goal

Create a clean product and delivery foundation before choosing an application stack or implementing an MVP feature.

## Decisions and tradeoffs

| Decision | Why | Alternatives considered | Consequences |
| --- | --- | --- | --- |
| Restart with an empty repository | The primary goal is to learn system design and make technology decisions consciously | Continue modifying the generated implementation | Previous implementation history was intentionally discarded; the project now starts from explicit decisions |
| Require pull requests for future changes | The product owner wants to review every change and use a collaborative engineering workflow | Commit directly to `main` | Changes gain a visible review history, with additional process overhead |
| Use automated approval only as the repository gate | Pull requests created through the owner's CLI identity cannot be approved by that same identity | Require a second human account or remove the approval rule | GitHub Actions satisfies the technical approval requirement, while the product owner retains the human review and merge decision |
| Organize work as an epic hierarchy | The MVP is too broad to reason about as a flat list of tickets | Use one large issue or unrelated feature issues | Requirements can be traced from the MVP to a domain epic and then to a focused ticket |
| Separate backlog grooming from active sprint work | Showing all unscheduled work on the delivery board would make the active flow noisy | Keep every issue in one board view | The backlog remains comprehensive while the sprint board shows only selected work |
| Delay technology selection until feature review | Choosing a complete stack up front would weaken the intended learning process | Select a conventional stack immediately | Each feature begins with an explicit architecture and tradeoff discussion |

## Work completed

- Recreated the public [Fridgely repository](https://github.com/YassineMessioui/Fridgely) and initialized its local `main` branch.
- Added the one-time bootstrap workflow and protected `main`. Pull requests require one approval, stale approvals are dismissed after new pushes, conversations must be resolved, and force pushes and branch deletion are disabled.
- Captured the complete product scope in [Epic #1: Fridgely Web MVP](https://github.com/YassineMessioui/Fridgely/issues/1).
- Created eight linked domain epics covering accounts, inventory, recipes, cooking, shopping, dashboard, web quality and security, and product validation.
- Created 37 focused feature tickets beneath those domain epics. Each ticket includes acceptance criteria and requires an architecture review before implementation.
- Created the public [Fridgely MVP Delivery project](https://github.com/users/YassineMessioui/projects/3).
- Configured a separate [Backlog view](https://github.com/users/YassineMessioui/projects/3/views/2) and a focused [Sprint Board](https://github.com/users/YassineMessioui/projects/3/views/1) with the flow `TODO → In Progress → Test Phase → Released / Done`.
- Added [Issue #47](https://github.com/YassineMessioui/Fridgely/issues/47) to track this opt-in journal foundation.

## Challenges and changes in direction

- A repository can only have truly zero commits by being deleted and recreated; deleting files in a new commit would preserve the earlier history.
- The local empty directory initially inherited Git metadata from a parent repository. Initializing a dedicated `.git` directory established the correct boundary.
- GitHub Projects requires a separate OAuth scope from repository management. That permission was added only after explicit approval.
- The first board design placed every item in a visible Backlog column. It was revised so backlog grooming and active sprint delivery have separate views.

## Validation

- GitHub reported the recreated repository as public and empty before the bootstrap commit.
- Local Git reported a clean `main` branch tracking `origin/main` after setup.
- GitHub recognized the pull-request approval workflow and confirmed the branch-protection settings.
- The project API confirmed the repository link, the issue count and hierarchy, the Backlog assignment, both project views, and all workflow statuses.

No application architecture or technology stack has been selected yet.

## Lessons

- Repository and delivery mechanics are architectural context: they shape how decisions are reviewed and recovered.
- A hierarchy is more useful than a flat backlog when product requirements span several domains.
- Keeping unscheduled work away from the sprint board makes current commitments easier to understand.
- Automation can satisfy a technical gate without replacing human judgment, as long as ownership of the final merge remains explicit.
- Deferring stack selection is valuable only when each future choice is recorded with its constraints and tradeoffs.

## Open questions

- Which minimal vertical slice should be selected for the first sprint?
- Which application shape, persistence approach, hosting model, and web technology best support that slice?
- Should architectural decisions live only in feature issues or also be preserved as repository Architecture Decision Records?

## Next steps

- Review and merge the development-journal pull request.
- Select a small set of inventory tickets for the first sprint.
- Compare architecture options for the first end-to-end inventory slice before implementation begins.
