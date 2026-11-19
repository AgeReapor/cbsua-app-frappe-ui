# CBSUA Frappe UI

CBSUA-maintained fork of [Frappe UI](https://github.com/frappe/frappe-ui), the Vue-based component library used by the Frappe application frontend. This repository exists to hold CBSUA-maintained UI-library changes that may be consumed by the forked Helpdesk frontend.

## Role in the CBSUA stack

- Provides shared Vue components, composables, utilities, and styling used by Frappe application interfaces.
- Is consumed as a Git submodule within [cbsua-app-helpdesk](https://github.com/AgeReapor/cbsua-app-helpdesk), rather than installed as a separate Frappe app.
- Is included indirectly when the Helpdesk source checkout and its submodules are used in local development or image builds.
- Is not a standalone service and is not independently installed on a Frappe site.

## Important submodule configuration note

At the time this README was prepared, the Helpdesk fork's `.gitmodules` file declares the submodule path as `frappe-ui` but its URL still points to the upstream `https://github.com/frappe/frappe-ui.git`. This means the Helpdesk repository's current submodule declaration does **not** itself select this CBSUA fork by URL.

Before relying on CBSUA-specific changes from this repository, reconcile the submodule URL and gitlink commit in `cbsua-app-helpdesk`, then verify the exact checked-out submodule SHA used by local Pilot and the deployment image. Do not assume that merely having this fork repository means the build consumes it.

## Development and integration

1. Make shared UI-library changes in this repository only when they are genuinely reusable across Frappe application interfaces.
2. Validate the library's tests, type checks, and production build using the scripts in `package.json`.
3. Update the Helpdesk submodule URL and gitlink deliberately if the CBSUA fork is intended to replace upstream.
4. Build and test the Helpdesk frontend from a clean checkout with submodules initialized.
5. Build the combined image through [cbsua-app-helpdesk-deployment](https://github.com/AgeReapor/cbsua-app-helpdesk-deployment) and verify the generated assets in the final image.

The package metadata identifies this as the `frappe-ui` package. Consult its own package scripts and documentation for exact development commands and dependency versions.

## Boundaries and maintenance

- Keep upstream attribution and licensing intact.
- Avoid introducing Helpdesk-only business logic into the shared UI library.
- Document API-breaking component changes and coordinate them with the Helpdesk frontend.
- Record the submodule commit SHA as part of release provenance.
- Prefer a small, reviewed fork delta over an untracked divergence from upstream.

## Related repositories

- [CBSUA Helpdesk](https://github.com/AgeReapor/cbsua-app-helpdesk) — consuming application and submodule owner.
- [CBSUA Helpdesk deployment](https://github.com/AgeReapor/cbsua-app-helpdesk-deployment) — combined image and release orchestration.
- [Upstream Frappe UI](https://github.com/frappe/frappe-ui) — original library.
