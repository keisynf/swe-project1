# Table Administration and Role Access 1-pager

## PROBLEM

Before service, Elena needs to keep a clear list of the restaurant’s tables so that servers can attach each new order to the correct place and staff can still identify a table on an older order. Reused or ambiguous table labels create mistakes during a busy shift. Deleting a table would also make an existing order harder to understand, so Elena needs a way to stop using a table for new service without losing its historical identity.

The shared application also needs to present the right workflow to each person. Priya uses a shared kitchen station, Daniel and Marcus use the server workflow, Elena uses the administrator view, and Maya only browses from a QR code. If roles can reach the wrong view, staff may perform actions outside their responsibilities or the administrator workflow may be exposed to people who should not use it.

## ASSUMPTIONS

- Elena creates and deactivates staff accounts and assigns each account a Server, Kitchen, or Admin role. The Kitchen role may be assigned to the shared kitchen-station account rather than an individual cook account.
- The product does not manage password reset or identity-provider integration. Those account-administration details are outside the vision and need a separate decision.
- A table label is a human-readable unique identifier. The vision does not define a format, numbering convention, or maximum length, so Elena must confirm those rules before implementation.
- Deactivating a table blocks only new-order selection. Existing orders retain their table label and can continue through their existing item-status and billing workflows.
- For access-flow usability testing, an 80% passing rate is an initial target that requires validation with Elena and staff before implementation.

## FUNCTIONAL REQUIREMENTS

- **As Elena, I want to maintain a list of uniquely labeled tables in the administrator view so that Daniel and Marcus can attach each new order to the correct table.**

  - Elena can maintain the table list from the administrator view.
  - Each table has a unique label.
  - A table has no seat-capacity attribute in this release.

- **As Elena, I want to deactivate a table instead of deleting it so that it cannot receive a new order but remains identifiable on its existing orders.**

  - Elena can deactivate a table from the administrator view.
  - A deactivated table cannot be selected for a new order.
  - The table label remains visible on its existing orders.

- **As Elena, I want to create and deactivate staff accounts and assign each account a role so that a new server can log in on the first day while former staff no longer have access.**

  - Elena can create and deactivate staff accounts from the administrator view.
  - Elena assigns each staff account one of the Server, Kitchen, or Admin roles.
  - A new server with an active Server account can log in to the server workflow on the first day.
  - A deactivated staff account cannot access its former workflow.
  - The Kitchen role may be assigned to the shared kitchen-station account rather than an individual cook account.

- **As Elena, I want the administrator view available only through the Admin role so that routine menu and table maintenance stays limited to the person responsible for it.**

  - Elena uses the Admin login to access the administrator view.
  - Server and Kitchen roles cannot access the administrator view.
  - The Server and Kitchen roles retain their permitted availability controls without receiving administrator-view access.

- **As Priya, I want to use one shared Kitchen station login so that the kitchen can use its queue and availability controls from the shared workstation without individual cook accounts.**

  - The Kitchen login identifies the shared station rather than an individual cook.
  - Priya can access the kitchen workflow and its permitted availability control through the Kitchen role.
  - The Kitchen role cannot access the administrator view.

## NON-FUNCTIONAL REQUIREMENTS

- **Role isolation:** Automated authorization tests must verify that Server and Kitchen credentials cannot access administrator-view routes or actions, that a guest session cannot access staff routes or actions, and that a deactivated staff account cannot access its former workflow.
- **Table identity integrity:** Automated integration tests must reject duplicate table labels and new-order use of a deactivated table while confirming that the label remains visible on previously created orders.
- **Access-flow usability:** In a moderated usability test, at least 80% of representative participants assigned a role can reach their permitted starting workflow and cannot mistake another role’s workflow for their own. The 80% target is an initial assumption that requires validation with Elena and staff before implementation.

## REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Elena maintains uniquely labeled tables | 5 | Requires a table data model, administrator workflow, uniqueness validation, persistence, and tests. The scope is bounded but establishes shared operational data. |
| Elena deactivates tables while preserving existing order identity | 5 | Requires lifecycle handling for table records, new-order validation, historical display behavior, and integration tests with orders. |
| Elena creates, deactivates, and assigns staff accounts | 8 | Requires staff-account lifecycle management, role assignment, active-account authorization, first-day login coverage, and tests for deactivation. The shared Kitchen station account adds a role-specific access path. |
| Elena uses the Admin-only administrator view | 5 | Requires role-based route and action authorization plus coverage for the availability-control exception. The underlying password-reset and identity-provider mechanisms remain out of scope. |
| Priya uses the shared Kitchen station login | 3 | Requires Kitchen-role routing and authorization for a shared station identity, plus tests that it cannot reach administrator capabilities. |
