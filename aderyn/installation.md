# Installation

{% hint style="warning" %}
**Aderyn is retired and is no longer maintained.** This page is retained at its existing URL for users following older installation links. Read the [retirement notice and removal guidance](https://aderyn.cyfrin.io/retirement).
{% endhint %}

### Installation and update status

* **Cyfrinup and GitHub releases:** Official Aderyn CLI installation and update downloads have been withdrawn. The retained installer scripts print a retirement notice and exit unsuccessfully. [Up](https://github.com/Cyfrin/Up) remains available for other Cyfrin tools.
* **Homebrew:** The `cyfrin/tap/aderyn` formula is disabled.
* **npm:** All published `@cyfrin/aderyn` versions are deprecated. Package archives may still be downloadable, but their installation scripts depend on withdrawn CLI downloads.
* **crates.io:** Aderyn's published crate versions are yanked. Yanking does not erase crate archives or invalidate existing lockfiles.

Do not use the former install or upgrade commands as a supported way to obtain Aderyn. The [retained documentation](https://aderyn.cyfrin.io/) is available for reference.

### Existing installations

Retirement does not uninstall existing copies. Remove Aderyn using the package manager that installed it, or follow the [removal guidance](https://aderyn.cyfrin.io/retirement) for a manually installed binary. Remove or replace Aderyn steps in maintained CI workflows as well.
