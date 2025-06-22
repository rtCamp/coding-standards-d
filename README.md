# `rtCamp Coding Standards D`

> The `D` is for David, the standards are for everyone.

![Packagist License](https://img.shields.io/packagist/l/rtCamp/coding-standards-d?color=green) ![Packagist Version](https://img.shields.io/packagist/v/rtCamp/coding-standards-d?label=stable) ![GitHub commits since latest release (by SemVer)](https://img.shields.io/github/commits-since/rtCamp/coding-standards-d/0.0.1) ![Tests](https://img.shields.io/github/actions/workflow/status/rtCamp/coding-standards-d/test.yml?branch=develop&label=CI)

-----

> [!WARNING]
> This is an unsanctioned project by @justlevine that is not (yet?) endorsed or supported by rtCamp.
> No one at rtCamp has been involved or consulted in any way before the creation of this project, neither about the project itself nor about any of the decisions made therein.
>
> Tl;dr this is just the _beginning_ of the conversation.

-----
This project is a collection of rules and sniffs for [PHPCS](https://github.com/PHPCSStandards/PHP_CodeSniffer) to validate code developed for Enterprise-grade WordPress projects. It uses rules from:
 - [WordPress Coding Standards](https://github.com/WordPress/WordPress-Coding-Standards)
 - [Automattic VIP Coding Standards](https://github.com/Automattic/VIP-Coding-Standards)
 - [Slevomat Coding Standard](https://https://github.com/slevomat/coding-standard)
 - [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility) & [PHPCompatibilityWP](https://github.com/PHPCompatibility/PHPCompatibilityWP)

## Why use Coding Standards?

Shared coding standards are a great way to ensure consistency in your codebase.

They help to avoid common pitfalls and mistakes, which in turn helps to reduce bugs and technical debt, and ensure all project contributors are following the same guidelines and best practices. Even better, it empowers us to spend less time writing, debugging, and reviewing code, and more time shipping important and scalable features.

> [!TIP]
> With the advent of AI-powered code assistants and agentic tools, having *strict and consistent coding standards* is more important than ever:
>
> - Codebase context is more important and provides more value than any `.cursorrules` or `.MD` reference file - this is true for both AI agents and human developers.
> - Agents can use the tooling directly to write better code specific to the standards and requirements of the specific codebase.
> - Developers can use the tooling to validate code written by AI agents (and their human peers) to prevent shipping hard-to-catch bugs and technical debt.

## Why use _these_ Coding Standards?

As the premier agency for Enterprise-grade WordPress development, rtCamp ensures that all code we write is high-quality, maintainable, and scalable. With hundreds of rtCampers around the world working on high-caliber projects, these rulesets ensure that _anybody_ at rtCamp can quickly jump into any project and ship quality code.

## Rulesets

The project provides a superset of sniffs that are tailored for the different needs of the common WordPress projects we work on.

Sniffs are grouped into different rulesets, allowing you to select the ones that make the most sense for the needs and constraints of your project. For example:

- A throwaway [migration-plugin](https://github.com/rtCamp/migration-plugin-skeleton-d) only needs the minimal set of sniffs to ensure that the code can run well on the target site and enable multiple developers to contribute to the codebase.
- A [feature plugin](https://github.com/rtCamp/features-plugin-skeleton-d) that is being handed-off to a client would benefit from autofixable sniffs, and the proper balance of functional sniffs to provide less-skilled developers the proper guardrails without slowing them down too much.
- A public plugin or theme should have strict rules - especially around documentation - and follow ecosystem patterns as much as possible. This helps the project's long-term maintainability, makes it easier for others to contribute to, all while serving as an example of best practices for the wider WordPress community.

You can also use `rtCamp` ruleset to get _all_ the checks.

You can use the following standard names when invoking `phpcs` to select the sniffs you want to use.

* [`rtCamp`](./rtCamp/ruleset.xml) - complete set with all of the sniffs in the project.

  - [`rtCamp-Minimum`](./rtCamp-Minimum/ruleset.xml): includes the minimum set of code quality and standard sniffs to ensure that your code is "enterprise-ready". **All** rtCamp code is expected to pass this ruleset.

  - [`rtCamp-Basic`](./rtCamp-Basic/ruleset.xml): includes all the sniffs in the `rtCamp-Minimum` ruleset, plus additional functional and autofixable sniffs that provide a good balance between code quality and developer experience. This is recommended for client projects where we don't know the skill level of the developers who will be maintaining the project after handoff.

  - [`rtCamp-Extra`](./rtCamp-Extra/ruleset.xml): includes all the sniffs in the `rtCamp-Basic` ruleset, plus additional standards and quality sniffs. This is recommended for internal projects where we want to ensure that the code is of the highest quality, but we don't need to be as strict as the `rtCamp-Strict` ruleset - e.g. when we know that the developers maintaining the project are experienced and familiar with the codebase.

  - [`rtCamp-Strict`](./rtCamp-Strict/ruleset.xml): includes all the sniffs in the `rtCamp-Basic` ruleset, plus additional functional sniffs to ensure that your code is of the highest quality and maintainability. This is recommended for public plugins and themes, or any project where you want to ensure the highest standards of code quality.

  - [`rtCamp-Docs`](./rtCamp-Docs/ruleset.xml): includes sniffs for doc-blocks and inline comments. This is recommended for any project where you want to ensure that your code is well-documented and easy to understand - by developers and AI agents alike,

## Installation

The recommended way to install this project is with [Composer](https://getcomposer.org/). Run the following command to install it into your project:

> [!IMPORTANT]
> Until this project is release publicly, you will need to add the repository to your `composer.json` file:
>
> ```json
> {
>   "repositories": [
>     {
>       "type": "vcs",
>       "url": "https://github.com/rtCamp/coding-standards-d.git"
>     }
>   ],
> }
> ```

```bash
composer require --dev rtCamp/coding-standards-d
```

This will install the latest compatible versions of PHPCS and _all the external sniffs and rulesets_, so there is no need to include them in your dependencies list.

We recommend the [PHP_CodeSniffer Standards Composer Installer Plugin](https://github.com/Dealerdirect/phpcodesniffer-composer-installer), which handles the registration of all of the installed standards, so there is no need to set the `installed_paths` config value manually, for single or multiple standards.

For more information about installation and usage, see the [WPCS readme](https://github.com/WordPress/WordPress-Coding-Standards#Installation).

## Configuring your custom ruleset.

> To quick-start your project, you can copy the [example config file](./phpcs.xml.dist.example) to your project root and rename it to `.phpcs.xml.dist`, then update the individual values as explained below.

The best way to use these sniffs in your project is to create a [local configuration file](https://github.com/PHPCSStandards/PHP_CodeSniffer/wiki/Advanced-Usage#using-a-default-configuration-file) that extends the rulesets provided by this project. When you name this file either `.phpcs.xml`, `phpcs.xml`, `.phpcs.xml.dist` or `phpcs.xml.dist`, PHP_CodeSniffer will automatically locate it as long as it is placed in the directory from which you run the CodeSniffer or in a directory above it.

In this file, you will want to configure the following:

- [`testVersion`](./phpcs.xml.dist.example#L33) - The minimum PHP version you want to test against. This should be the _lowest version of PHP that you want to support_. While WordPress officially supports PHP 7.2+ we recommend PHP 8.2+ unless you have a specific reason to support older versions (e.g. a public plugin or legacy project).
- [`minimum_wp_version`](./phpcs.xml.dist.example#L43) - The minimum WordPress version you want to test against. This should be the lowest version of WordPress that you want to support. For client projects, this is usually the version of WordPress that the client is usually using.
- [`WordPress.WP.I18n.text_domain`](./phpcs.xml.dist.example#L63) - The text domain used in your project. This is used by the `WordPress.WP.I18n` sniff to check that all translatable strings are assigned to a text domain. We recommend using the format `rt-<project-name>`.
- [`WordPress.NamingConventions.PrefixAllGlobals`](./phpcs.xml.dist.example#L57) - The list of prefixes used in your project. This is used by the `WordPress.NamingConventions.PrefixAllGlobals` sniff to check that all global functions, classes, constants, and variables are prefixed.

## Special Configurations

### Non-WPVIP Hosts

[ @todo ]

### PSR-4-style Autoloading

[ @todo ]

## Development and Support

@TODO add a CONTRIBUTING.md / DEVELOPMENT.md

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
> If you want to ensure that no linting errors are introduced when updating child dependencies (e.g. with `composer update -W` ), make sure to add the specific libary to your own `composer.json:devDependencies` and pin it with a `~` version constraint, e.g. `"automattic/vipcs": "~3.1.0"`.

## Care about quality code?
<a href="https://rtcamp.com/"><img src="https://rtcamp.com/wp-content/uploads/sites/2/2019/04/github-banner@2x.png" alt="Join us at rtCamp, we specialize in providing high performance enterprise WordPress solutions"></a>
