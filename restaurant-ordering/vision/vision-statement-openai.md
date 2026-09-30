# Product Vision — Restaurant Ordering and Status Platform

**Status:** Draft  
**Restaurant context:** One casual-dining restaurant

## Vision Statement

For guests, servers, kitchen staff, administrators, and the owner-operator at one casual-dining restaurant, the Restaurant Ordering and Status Platform provides one shared, accurate view of the current menu and every order. Guests use a generic QR code to browse the latest available menu; the QR code identifies neither a table nor a guest. Servers select a table when creating an order, manage service progress, generate bills, and confirm delivery. Kitchen staff receive orders, manage preparation, and report unfulfillable items. Administrators maintain menu and table data. Unlike disconnected paper tickets, verbal updates, or separate manual tracking tools, the platform keeps menu availability, order progress, delivery completion, and bill totals current for the staff who need them, reducing uncertainty about what was ordered, what is ready, and what has reached the guest.

## Product Scope for the Initial Release

### In scope

- A generic, QR-code-accessible, view-only digital menu for guests. QR codes do not distinguish tables or identify guests.
- Guest menu categories, item names, descriptions, tax- and service-inclusive prices, availability, and modifiers. Dietary information is not included in this release.
- Server-created and server-managed orders. Each order is attached to exactly one table selected by the server from the active table list. Guests cannot create or modify orders.
- A table list managed by administrators. Each table has a unique label, has no seat-capacity attribute, and is deactivated rather than deleted. A deactivated table cannot be selected for a new order but remains identifiable on its existing orders.
- Item statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, and **rejected**.
- Order statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, **rejected**, and **closed**.
- A kitchen view that receives server-created orders and updates item preparation states.
- A server view for selecting a table, entering orders, monitoring item and order statuses, confirming delivery, generating bills, and closing orders.
- A server-only bill that lists ordered items, selected modifiers, quantities, and the total. All menu prices include tax and service; the system stores no tax rate and the bill shows no separate tax or service amount. The bill does not include tip suggestions and does not process payments.
- Menu availability controls for administrators, servers, and kitchen staff. Marking an item unavailable immediately removes it from the guest menu and blocks it from being added to new orders. An item already on an order remains on that order; kitchen staff reject it if it cannot be prepared.
- A kitchen rejection workflow with an optional free-text reason visible to the server.
- An in-app kitchen alert when a server cancels an item that is already **preparing**. Alerts are not pushed to locked or sleeping devices.
- Login-based roles: **Server**, **Kitchen**, and **Admin**. Servers and administrators use their role login; kitchen staff use one shared kitchen-station login. Guests have no account or login. Only **Admin** can access the administrator view. Servers and kitchen staff can use the availability toggle from their own views without gaining administrator-view access.
- An administrator view for managing menu categories, item names, descriptions, prices, availability, modifiers, and the table list.
- A standalone application for one restaurant.

### Out of scope

- Guest-initiated ordering, order changes, or bill access.
- QR codes that identify a table, guest, or order.
- Dietary information.
- Payment processing, tip suggestions, tax calculations, service-charge calculations, or tax-rate storage.
- Device or lock-screen push notifications for cancellation alerts.
- POS, inventory, or third-party kitchen-display-system integrations.
- Multi-location or multi-restaurant management.

## Order Lifecycle

### Item states and transition ownership

| Item status | Meaning | Who can set it |
|---|---|---|
| **placed** | The item has been added to an order and is awaiting kitchen work. | A server creates the item in this status. |
| **preparing** | The kitchen has started work on the item. | Kitchen staff move a placed item to this status. |
| **ready** | The kitchen has completed the item and it can be taken to the guest. | Kitchen staff move a preparing item to this status. |
| **delivered** | The item has reached the guest. | A server moves a ready item to this status. |
| **canceled** | The item will not be fulfilled because the server canceled it. | A server can cancel an item before it is delivered. If the item is **preparing**, the kitchen receives an in-app alert. |
| **rejected** | The item cannot be fulfilled by the kitchen. | Kitchen staff reject an item they cannot fulfill before it is delivered and may provide an optional free-text reason visible to the server. |

The standard item path is **placed** → **preparing** → **ready** → **delivered**. **Canceled** and **rejected** are terminal exceptions. A server may cancel an item before it is delivered; kitchen staff may reject an item before it is delivered when the kitchen cannot fulfill it.

### Order status derivation and closure

The system derives each order status from its items, rather than requiring staff to set the order status separately. In these rules, a *fulfillable item* is an item that is neither canceled nor rejected. The system evaluates the following rules in the stated order. The first matching rule determines the order status, except that **closed** is a server-set final state that overrides the derived status.

| Order status | Derivation or closure rule |
|---|---|
| **closed** | A server explicitly closes an order only after it is **delivered** and the server has generated its final bill. A closed order cannot receive further item changes. |
| **rejected** | No fulfillable items remain, and every item is **rejected**. |
| **canceled** | No fulfillable items remain, every item is terminal (**canceled** or **rejected**), and at least one item is **canceled**. |
| **delivered** | At least one fulfillable item exists, and every fulfillable item is **delivered**. |
| **ready** | At least one fulfillable item is **ready**, and every fulfillable item is either **ready** or **delivered**. This means kitchen work is complete even when a server has already delivered some items. For example, delivered drinks and ready mains produce an order status of **ready**. |
| **placed** | At least one fulfillable item exists, and every fulfillable item is **placed**. |
| **preparing** | The order did not match any earlier rule and has at least one fulfillable item. This covers any mixed active state, including an item that is **preparing**, or a combination of **placed**, **preparing**, **ready**, and **delivered** items that still has outstanding kitchen or delivery work. **Preparing** is the single kitchen-working term for both items and orders. |

These rules are mutually exclusive when evaluated in precedence order. In particular, an order that contains only **ready** and **delivered** fulfillable items is always **ready**, not **preparing**. **Closed** separates food-service completion from bill completion: an order is **delivered** when every fulfillable item has reached the guest, then becomes **closed** only when a server generates the final bill and marks the delivered order as closed. Closing does not mean that payment was processed.

## Non-Functional Requirements

- **Mobile QR-menu performance.** **Assumption:** At the 95th percentile, a supported phone on a stable 4G or Wi-Fi connection renders the guest menu's available categories and items within **2 seconds** of opening the QR-code URL. The **2-second** target is an initial assumption to validate with the restaurant and representative devices and networks.

## Product Principles

1. **One current operational record.** Staff should see status, availability, and table changes without relying on verbal handoffs or duplicate tracking.
2. **Menu accuracy at the point of browsing and ordering.** Guests and servers should see current categories, item descriptions, tax- and service-inclusive prices, available items, and modifiers. Unavailable items cannot be added to new orders.
3. **Role-appropriate workflows.** Guests browse without an account; servers select tables and manage orders and bills; kitchen staff manage preparation, availability, and rejection; administrators maintain menu and table data.
4. **Clear completion signals.** **Ready** means an item can leave the kitchen. **Delivered** means it has reached the guest. **Closed** means the server has completed billing work without implying payment was collected.
5. **Simple initial operations.** The first release prioritizes coordinated service for one restaurant rather than payments, integrations, or enterprise capabilities.

## Intended Outcome

Restaurant staff can reliably answer, at any moment, what each table ordered, whether each item is placed, preparing, ready, delivered, canceled, or rejected, whether the order is ready, delivered, or closed, and what the tax- and service-inclusive total is for a server-generated bill.

## Business Buyer and Value

The owner-operator is the business buyer. The owner-operator decides whether to adopt and pay for the platform and whether to keep it after launch. The restaurant should gain fewer avoidable order and availability mistakes, less manual coordination between servers and the kitchen, faster onboarding for new staff, and more consistent service. The owner-operator will continue paying only if those operating benefits outweigh the product's cost and the effort of keeping it current.