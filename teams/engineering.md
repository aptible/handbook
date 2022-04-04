# Engineering at Aptible

## Project Management

The Engineering Team uses [Shortcut](https://shortcut.com/) for tracking work, 
[following the same structure as the rest of Aptible](https://github.com/aptible/handbook/blob/main/how-we-work/sprint-project-management.md).

Outside of the company-wide meetings, the Engineering Team has a 
few team-specific meetings related to project management:
* Backlog grooming: Every few weeks (as needed), we have one longer meeting where we talk through Epics and 
  Stories that are ready for development to ensure that everyone understands what’s coming up. 
  The day before this call a list of everything that’s ready to be groomed will be shared with the Engineering Team.
  Everyone on the team should review this list asynchronously, and come prepared with suggestions or questions to 
  ensure we can make the most of our synchronous discussion time. 
  * As new projects come up, we may also do one-off grooming sessions for those projects depending on 
    the priority, complexity, and importance of the project.
* Sprint planning: On the last day of each Sprint, we have a 30 minute meeting where we decide what the primary 
  goals are for next Sprint, and what everyone is committing to in working toward those goals.
* Daily Syncs: Daily 15-30 minute meetings where we talk about what we’re working on right now. 
  The primary purpose of this call is to ensure that everyone is able to focus on their goals, 
  course correct (or update goals) when they’re not, and identify areas where others can collaborate 
  or unblock each other. During these syncs, we should always be 
  referring back to both Shortcut and the goals we set for this Sprint.

## Contributing Code

Outside of internal-only documentation repositories, 
all new contributions and repositories should follow the following guidelines.
It's recommended that you follow these guidelines for important changes to internal-only 
documentation repositories too, but it's not required.

With the exception security-related guidelines, which all repositories and contributions should follow,
there’s a chance that some older repositories and contributions don't meet these guidelines. 
Updating repositories that existed prior to these guidelines will take time.
Feel free to make small, incremental changes that get us closer to our our ideal when working on these repositories.

### Repository management

* Outside of small changes, every commit and/or PR should 
  [reference a Shortcut story](https://github.com/aptible/handbook/blob/10a21bc3d2dbe0281b9fda74107442924a17af99/how-we-work/using-shortcut.md#github--shortcut-integration-aka-automatically-updating-stories-via-github-commits).
* Every repository should have a README that provides:
  * A high level overview of what the code does.
  * Instructions for how to run the code locally.
  * Instructions for how to run tests locally.
  * Instructions for how to deploy/run the code in all environments.
  * Context for how and where this code is run in production (e.g. ECS, Aptible App, or on an EC2 instances).
* Production repositories should have one or more protected branches 
  (the preferred branch is `main`) which code is built or deployed from. 
  The following protections should be in place:
  * Require a pull request before merging
  * Require approvals (1 approval is sufficient)
  * Dismiss stale pull request approvals when new commits are pushed
  * Require status checks to pass before merging
* Repositories that are no longer in use should be archived. This is **especially** important
  if it is a public repository.
* All production repositories must have relevant security tooling enabled. Snyk is preferred, although
  in places where it may not be appropriate (e.g. some public repositories) Dependabot is acceptable.
  * Where possible, scanning and remediation should happen automatically, and not just when a new PR is opened.

### Pull requests

* PRs should contain enough context that anyone on the Engineering Team is able to understand why changes are
  being made as well as review and test changes. This should be done even if a specific reviewer already has
  all the required context.
* Prior to merging a PR into a protected branch, all tests should be passing, and the changes should 
  be approved by another Aptible team member.
* For high risk security changes, PRs require approval of at least two reviewers. 
  One reviewer should be doing a general code review (including security), and the other reviewer 
  should be doing a security-focused review.
  * Whether or not a change is high risk is determined by the code author. When in doubt, assume a change is high risk.
* There may be rare exceptions where we need to merge code without passing tests.
  The reason for the exception should be documented somewhere in the PR.

#### PR review expectations

* PRs should be reviewed within 24 hours. If the reviewer is unable to do an initial review
  in that time frame, the reviewer should work with the author to either find another reviewer
  or determine a reasonable time frame for review.
* Any PRs open for more than a week should either have active conversation on the PR, or have a comment
  explaining why the PR is still open.

### CI/CD

* For every language that supports linting, code linting should be built into the testing process.
* For Ruby, we should use the Rubocop rules defined in aptible-tasks.
* Code deployed to production should be deployed from a protected branch.
  * There rarely may be special edge cases to this rule. Those edge cases need to be approved in #security
    prior to deployment.
* Any changes that heavily leverage interaction between services (the primary example of this being 
  interacting with cloud provider APIs) should have integration tests.

### Adding open source tools, libraries, and packages

In most cases, we don't have set policy for how to determine which tools, libraries, and packages
we're willing to adopt. This comes up infrequently enough that if you'd like to add a new tool, library,
or package to our ecosystem, you should just ask in #engineering or #security. 
Ideally, when you ask, you should already be able to answer questions like:
* Why do we want to do this?
* Do we already do something similar today? Why can't we continue to use that?
* Why is this the right tool for what you're trying to accomplish? What alternatives exist?
* How maintained is the project?
* How trusted are the maintainers?
* What does the security history look like? Are they clearly acknowledging and patching security issues?
* Do they frequently have security issues? 
* Do they reports security issues in high-visibility places that are easy to track?

There are two exceptions to this, where we do have a known policy:
* For Fluentd, we should prefer plugins maintained by a well-known company, followed 
  by [Certified](https://www.fluentd.org/faqs#certified) plugins.
* For GitHub Actions, only Actions maintained by Aptible, GitHub, or Github-Verified Creators can be used.

## Documentation

* Repository-specific documentation related to how to use, test, and deploy the repository belongs in the repository
  itself.
* Random one-off scripts should live in `aptible/scripts` or in the repository associated with those scripts.
* More extensive documentation and runbooks should live in `aptible/handbook-internal`.
* Highly collaborative one time docs (e.g. Post Mortems, design docs) should live in the correct Shared drive in
  Google Drive. Most of the time this will either be the `Engineering` or `Security and Compliance` Shared drive.
