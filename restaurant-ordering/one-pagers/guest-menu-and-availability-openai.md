# Guest Menu and Availability 1-pager

## PROBLEM

When Maya arrives for dinner, she wants to scan the restaurant’s QR code, see what can actually be ordered, and decide before the server comes to the table. If the menu is slow, omits descriptions or prices, or shows an item that the kitchen has run out of, she must ask staff for information that the menu should already provide. That wastes time for Maya and creates avoidable work for Daniel and Priya during service.

Elena needs to maintain the menu once and have every person use the same current information. Daniel and Priya also need to remove an unavailable item during a shift, while Marcus needs to recognize that an item cannot be added before he records a guest’s request. The capability must update the guest menu and order-entry view consistently without changing items that were already ordered.

## ASSUMPTIONS

- At the 95th percentile, a supported phone on a stable 4G or Wi-Fi connection renders the available menu categories and items within **2 seconds** of opening the generic QR-code URL. This is the vision’s initial target and requires validation with the restaurant and representative devices and networks.
- On a stable network connection, an availability change appears in the relevant active guest and server views within **3 seconds at the 95th percentile**, measured from confirmation of the change to display of the result. This proposed target requires validation before implementation.
- The vision does not decide the ordering of categories or items, searching, filtering, images, or the presentation of modifiers. This release assumes no search, filter, or image capability; category and item ordering must be confirmed with Elena before implementation.
- An unavailable item remains on an existing order unchanged. Priya rejects the existing item only if the kitchen cannot fulfill it; changing availability does not automatically reject it.

## FUNCTIONAL REQUIREMENTS

- **As Maya, I want to open the generic QR-code menu and browse available categories and items so that I can decide what to ask Daniel to order without waiting for basic menu or availability information.**

  - Maya can access the view-only menu without an account or login.
  - The generic QR code identifies neither Maya nor her table.
  - The menu shows available categories and available items, including each item’s name, description, tax- and service-inclusive price, and modifiers.
  - The menu does not let Maya create or modify an order, see an order status, access a bill, or make a payment.

- **As Elena, I want to maintain menu categories, items, descriptions, prices, modifiers, and availability in the administrator view so that the restaurant can keep one current menu without duplicate entry or an external system.**

  - Elena can manage categories, item names, descriptions, tax- and service-inclusive prices, modifiers, and availability from the administrator view.
  - The product stores no tax rate and does not calculate tax or service charges separately.
  - Dietary information is not included in this release.
  - An item’s availability change is reflected in the guest menu and server order-entry view under the availability-update assumption.

- **As Daniel, I want to mark an item unavailable from the server view so that I do not take a new order for something the restaurant cannot provide.**

  - Daniel can toggle availability from the server view without access to the administrator view.
  - An unavailable item is removed from the guest menu and cannot be added to a new order.
  - Daniel’s availability change does not alter an item already on an order.

- **As Priya, I want to mark an item unavailable from the kitchen view so that new orders stop requesting an item the kitchen cannot make.**

  - Priya can toggle availability from the kitchen view without access to the administrator view.
  - An unavailable item is removed from the guest menu and cannot be added to a new order.
  - Priya rejects an existing ordered item only when the kitchen cannot fulfill it.

- **As Marcus, on my first server shift, I want to recognize when an item is unavailable before I enter a guest’s request so that I do not promise food the kitchen cannot make.**

  - The server order-entry view identifies currently unavailable items.
  - Marcus cannot add an unavailable item to a new order.
  - Marcus can use the same availability information that Maya sees in the guest menu.

## NON-FUNCTIONAL REQUIREMENTS

- **Mobile menu performance:** Under the mobile-performance assumption, at least 95% of supported-device test runs render the available categories and items within 2 seconds after opening the QR-code URL. Verify this with timestamped browser tests on representative supported phones and stable 4G or Wi-Fi connections.
- **Availability freshness:** Under the availability-update assumption, at least 95% of tested availability changes appear in active guest and server views within 3 seconds, without reopening a view. Verify this with timestamped end-to-end tests.
- **Availability integrity:** Automated integration tests must prevent an unavailable item from being added to a new order while preserving the same item on orders created before the availability change.

## REQUIREMENTS SIZING

Sizing uses Fibonacci story points. **One point represents one day or less of well-understood implementation work.** Estimates include implementation, focused tests, and uncertainty in the existing application architecture.

| Story | Estimate | Rationale |
|---|---:|---|
| Maya browses the generic QR menu | 8 | Requires a mobile view-only menu, QR entry point, categories, item details, modifiers, availability display, and responsive testing. The mobile performance target adds cross-device verification. |
| Elena maintains menu information | 8 | Requires administrator workflows for several related menu attributes, validation, persistence, and propagation to the guest and server views. The work spans a central data model and multiple views. |
| Daniel toggles availability | 3 | Reuses the shared availability capability but requires a server-view control, permission enforcement, propagation, and tests. |
| Priya toggles availability | 3 | Reuses the shared availability capability but requires the kitchen-view control and kitchen-specific permission coverage. |
| Marcus recognizes unavailable items | 3 | Reuses the availability data but requires deliberate server-view presentation and first-shift usability validation. |
