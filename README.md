# rtCamp Coding Standards D

> The `D` is for David, the standards are for everyone.

-----

> [!WARNING]
> This is an experimental project by @justlevine that is not (yet?) endorsed or supported by rtCamp.

-----

A compact collection of PHPCS rulesets and sniffs for enterprise WordPress projects. It combines and curates rules from:

 - [WordPress Coding Standards](https://github.com/WordPress/WordPress-Coding-Standards)
 - [Automattic VIP Coding Standards](https://github.com/Automattic/VIP-Coding-Standards)
 - [Slevomat Coding Standard](https://https://github.com/slevomat/coding-standard)
 - [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility) & [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP)

## Why use Coding Standards?

Shared coding standards are a very effective way to ensure consistency in your codebase.

They help to avoid common pitfalls and mistakes, which in turn helps to reduce bugs and technical debt, and ensure all project contributors are following the same guidelines and best practices. Even better, it empowers us to spend less time writing, debugging, and reviewing code, and more time shipping important and scalable features.

> [!NOTE]
> With the advent of AI-powered code assistants and agentic tools, having *strict and consistent coding standards* is more important than ever:
>
> - Codebase context provides more value than any `AGENTS.md` reference file or Claude Skills; this is true for both AI agents and human developers.
> - Agents can use the tooling directly to write better code specific to the standards and requirements of the specific codebase.
> - Developers can use the tooling to validate code written by AI agents (and their human peers) to prevent shipping hard-to-catch bugs and technical debt.

## Why use _these_ Coding Standards?

- Ensure consistent, maintainable code across teams.
- Catch common bugs and reduce technical debt.
- Provide autofixable sniffs and practical guardrails for developers and AI tools.

## Rulesets

- [`rtCamp`](rtCamp/ruleset.xml): the full superset. It includes all rules from the other sets, and is designed to be comprehensive while still practical for most projects. We recommend starting with this and then customizing as needed. **Use this by default.** 

  - [`rtCamp`](./rtCamp/ruleset.xml) - complete set with all of the sniffs in the project.

    🎯 Use this ruleset unless you have a particular reason to use or compose the others.

  - [`rtCamp-Minimum`](./rtCamp-Minimum/ruleset.xml): includes the minimum set of code quality and standard sniffs to ensure that your code is "enterprise-ready". **All** rtCamp code is expected to pass this ruleset.

  - [`rtCamp-Basic`](./rtCamp-Basic/ruleset.xml): includes all the sniffs in the `rtCamp-Minimum` ruleset, plus additional functional and autofixable sniffs that provide a good balance between code quality and developer experience. This is recommended for client projects where we don't know the skill level of the developers who will be maintaining the project after handoff.

  - [`rtCamp-Extra`](./rtCamp-Extra/ruleset.xml): includes all the sniffs in the `rtCamp-Basic` ruleset, plus additional standards and quality sniffs. This is recommended for internal projects where we want to ensure that the code is of the highest quality, but we don't need to be as strict as the `rtCamp-Strict` ruleset - e.g. when we know that the developers maintaining the project are experienced and familiar with the codebase.

  - [`rtCamp-Strict`](./rtCamp-Strict/ruleset.xml): includes all the sniffs in the `rtCamp-Basic` ruleset, plus additional functional sniffs to ensure that your code is of the highest quality and maintainability. This is recommended for public plugins and themes, or any project where you want to ensure the highest standards of code quality.

  - [`rtCamp-Docs`](./rtCamp-Docs/ruleset.xml): includes sniffs for doc-blocks and inline comments. This is recommended for any project where you want to ensure that your code is well-documented and easy to understand - by developers and AI agents alike,

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

- Non-WPVIP hosts: [TODO]
- PSR-4 autoloading: [TODO]
- Test files: [TODO]

## Development & support

Add a `CONTRIBUTING.md` or `DEVELOPMENT.md` when ready. Meanwhile, open issues on GitHub or contact David Levine.


## Versioning

This project follows [Semantic Versioning](https://semver.org/). The version number is composed of three parts: `MAJOR.MINOR.PATCH`. The MAJOR version is incremented for breaking changes, the MINOR version is incremented for new features, and the PATCH version is incremented for bug fixes.

In the context of code quality tooling, it's not always clear what constitutes a breaking change. We use the following guidelines by [Eslint](https://github.com/eslint/eslint/?tab=readme-ov-file#semantic-versioning-policy) ), where:

- **PATCH** releases are for bug fixes, rereleases, documentation updates, and other non-user-facing changes that are _intended to not break your lint build_.
- **MINOR** releases are for adding new rules or sniffs to support new language features, deprecating or fixing existing rules, and _might_ break your lint build if you were relying on the previous behavior of a sniff.
- **MAJOR** releases are making breaking changes [such as](https://github.com/WordPress/WordPress-Coding-Standards/issues/1703#issuecomment-492014220):
  - Changes to the names of rulesets and/or splitting rulesets.
  - Adding or removing rules from a ruleset, or moving rules between rulesets.
  - SemVer major version bumps to the Composer dependencies.

Per the above, any minor update may report more linting errors than the previous release (ex: from a bug fix). For projects without a lockfile, we recommend using the tilde (~) in `composer.json` to ensure that you get the latest patch release of the minor version you are using, e.g. `"rtcamp/coding-standards-d": "~1.1.0"`.

> [!IMPORTANT]
> The above applies to most PHPCS ruleset libraries, including those we use in this project.
>
> If you want to ensure that no linting errors are introduced when updating child dependencies (e.g. with `composer update -W` ), make sure to add the specific library to your own `composer.json:devDependencies` and pin it with a `~` version constraint, e.g. `"automattic/vipcs": "~3.1.0"`.

## Care about quality code?
<a href="https://rtcamp.com/"><img src="https://rtcamp.com/wp-content/uploads/sites/2/2019/04/github-banner@2x.png" alt="Join us at rtCamp, we specialize in providing high performance enterprise WordPress solutions"></a>
