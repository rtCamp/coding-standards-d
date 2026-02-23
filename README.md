# rtCamp Coding Standards D

> The `D` is for David, the standards are for everyone.

---

> [!WARNING]
> This is an experimental project by @justlevine that is not (yet?) endorsed or supported by rtCamp.

---

A compact collection of PHPCS rulesets and sniffs for enterprise WordPress projects. It combines and curates rules from:

- [WordPress Coding Standards](https://github.com/WordPress/WordPress-Coding-Standards)
- [Automattic VIP Coding Standards](https://github.com/Automattic/VIP-Coding-Standards)
- [Slevomat Coding Standard](https://https://github.com/slevomat/coding-standard)
- [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility) & [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP)

## Why use Coding Standards?

Consistent coding standards reduce bugs, prevent common mistakes, and lower technical debt. They speed up reviews and maintenance so teams can ship reliably. Most importantly, they let us spend us to spend less time writing, debugging, and reviewing code, and more time shipping important and scalable features.

> [!NOTE]
> AI code assistants and agentic tools make _strict and consistent_ coding standards more important than ever:
>
> - A project's codebase and tooling provide stronger context and guardrails than any `AGENTS.md` or external skill docs.
> - Agents and harnesses can use the tooling directly to write higher-quality code that follows the project's standards and conventions.
> - Developers can quickly validate agent-generated code to avoid subtle bugs.

## Why use _these_ Coding Standards?

- Ensure consistent, maintainable code across teams.
- Catch common bugs and reduce technical debt.
- Provide autofixable sniffs and practical guardrails for developers and AI tools.

## Rulesets

- [`rtCamp`](rtCamp/ruleset.xml): the full superset with all of the sniffs in the project.

    🎯 **Use this by default** and customize as needed, unless you have a particular reason to use or compose the others.

- [`rtCamp-Minimum`](./rtCamp-Minimum/ruleset.xml): Essential sniffs for enterprise-ready code. All rtCamp code should pass this.

- [`rtCamp-Basic`](./rtCamp-Basic/ruleset.xml): Everything in `rtCamp-Minimum` plus practical, autofixable sniffs. This is recommended for client projects where we don't know the skill level of the developers who will be maintaining the project after handoff.

- [`rtCamp-Extra`](./rtCamp-Extra/ruleset.xml): `rtCamp-Basic` plus additional quality-focused sniffs for internal projects that prioritize higher standards without `rtCamp-Strict`'s rigidity.

- [`rtCamp-Strict`](./rtCamp-Strict/ruleset.xml): `rtCamp-Basic` plus stricter functional sniffs for maximum quality and maintainability.  This is recommended for public plugins and themes, or any project where you want to ensure the highest standards of code quality.

- [`rtCamp-Docs`](./rtCamp-Docs/ruleset.xml): Doc-block and comment sniffs to ensure clear, well-documented code. This is recommended for any project where you want to ensure that your code is well-documented and easy to understand - by developers and AI agents alike.

## Installation

Recommended via [Composer](https://getcomposer.org/):

```bash
composer require --dev rtCamp/coding-standards-d
```

This will install the latest compatible versions of PHPCS and _all the external sniffs and rulesets_, so there is no need to include them in your dependencies list.

We recommend the [PHP_CodeSniffer Standards Composer Installer Plugin](https://github.com/Dealerdirect/phpcodesniffer-composer-installer), which handles the registration of all of the installed standards, so there is no need to set the `installed_paths` config value manually, for single or multiple standards.

For more information about installation and usage, see the [WPCS readme](https://github.com/WordPress/WordPress-Coding-Standards#Installation).

## Configuring your project

> [!TIP]
> To quick-start your project, you can copy the [example config file](./phpcs.xml.dist.example) to your project root and rename it to `.phpcs.xml.dist`, then update the individual values as explained below.

Key settings to configure in your local file:

- `testVersion`: minimum PHP version to test (we recommend PHP 8.2+ unless constrained).
- `minimum_wp_version`: lowest WordPress version you support.
- `WordPress.WP.I18n.text_domain`: recommended format `rt-<project-name>`.
- `WordPress.NamingConventions.PrefixAllGlobals`: list of project prefixes.

## Special configurations

- Non-WPVIP hosts: [@todo]
- PSR-4 autoloading: [@todo]
- Test files: [@todo]

## Development & support

Add a `CONTRIBUTING.md` or `DEVELOPMENT.md` when ready. Meanwhile, open issues on GitHub or contact David Levine.

## Versioning

This project follows [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`), where:

- **MAJOR**: breaking changes.
- **MINOR**: new rules, deprecations, or behavior changes that may increase lint errors.
- **PATCH**: bug fixes, docs, and other non-breaking tweaks.

Because code quality tooling can make "breaking" ambiguous, we follow [Eslint's policy](https://github.com/eslint/eslint/?tab=readme-ov-file#semantic-versioning-policy) ):

- **PATCH** releases are for bug fixes, rereleases, documentation updates, and other non-user-facing changes that are _intended to not break your lint build_.
- **MINOR** releases may add new rules/sniffs and deprecate or fix existing rules, and _might_ cause existing code to fail linting.
- **MAJOR** release contain breaking changes such as: renaming/splitting rulesets, adding/removing/moving rules, or major dependency bumps. These changes may cause existing code to fail linting and require changes to your config or CI workflow.

Minor releases may increase reported linting errors. For projects without a lockfile, pin the dependency with a tilde(`~`) in `composer.json` to receive patch updates only, e.g. "rtcamp/coding-standards-d": "~1.1.0".

> [!IMPORTANT]
> These guidelines apply to most PHPCS ruleset libraries, including those we use in this project.
>
> To avoid new lint errors when updating child dependencies (for example via `composer update -W`), add the library to your project's dev dependencies and pin it with `~` as well, e.g. "automattic/vipcs": "~3.1.0".

## Care about quality code?

<a href="https://rtcamp.com/"><img src="https://rtcamp.com/wp-content/uploads/sites/2/2019/04/github-banner@2x.png" alt="Join us at rtCamp, we specialize in providing high performance enterprise WordPress solutions"></a>
