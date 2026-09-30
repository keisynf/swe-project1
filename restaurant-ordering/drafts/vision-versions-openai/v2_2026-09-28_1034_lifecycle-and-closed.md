# Product Vision — Restaurant Ordering and Status Platform

**Status:** Draft  
**Restaurant context:** One casual-dining restaurant

## Vision Statement

For guests, servers, kitchen staff, and restaurant administrators at one casual-dining restaurant, the Restaurant Ordering and Status Platform provides one shared, accurate view of the current menu and every order. Guests use a generic QR code to browse the latest available menu; the code does not identify a table or a guest. Servers create and manage orders, generate bills, and confirm delivery. Kitchen staff receive orders and manage preparation. Unlike disconnected paper tickets, verbal updates, or separate manual tracking tools, the platform keeps menu availability, order progress, delivery completion, and bill totals current for the staff who need them, reducing uncertainty about what was ordered, what is ready, and what has reached the guest.

## Product Scope for the Initial Release

### In scope

- A generic, QR-code-accessible, view-only digital menu for guests. QR codes do not distinguish tables or identify guests.
- Server-created and server-managed orders. Guests cannot create or modify orders.
- Item statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, and **rejected**.
- Order statuses: **placed**, **preparing**, **ready**, **delivered**, **canceled**, **rejected**, and **closed**.
- A kitchen view that receives server-created orders and updates item preparation states.
- A server view for entering orders, monitoring item and order statuses, confirming delivery, generating bills, and closing orders.
- A server-only bill that lists ordered items, selected modifiers, quantities, and the total. Item prices are tax-inclusive, so the bill does not show a separate tax amount. The bill does not include tip suggestions and does not process payments.
- An administrator view for managing menu categories, items, availability, and modifiers.
- A standalone application for one restaurant.

### Out of scope

- Guest-initiated ordering, order changes, or bill access.
- QR codes that identify a table, guest, or order.
- Payment processing.
- Separate tax calculations or tip suggestions on bills.
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
| **canceled** | The item will not be fulfilled because the server canceled it. | A server can cancel an item before it is delivered. |
| **rejected** | The item cannot be fulfilled by the kitchen. | Kitchen staff reject an item they cannot fulfill before it is delivered. |

The standard item path is **placed** → **preparing** → **ready** → **delivered**. **Canceled** and **rejected** are terminal exceptions. A server may cancel an item before it is delivered; kitchen staff may reject an item before it is delivered when the kitchen cannot fulfill it.

### Order status derivation and closure

The system derives each order status from its items, rather than requiring staff to set the order status separately. In these rules, a *fulfillable item* is an item that is neither canceled nor rejected.

| Order status | Derivation or closure rule |
|---|---|
| **placed** | Every fulfillable item is **placed**. |
| **preparing** | At least one fulfillable item is **preparing** or **ready**, but the order does not yet meet the rule for **ready**. This is the single kitchen-working state for orders and items. |
| **ready** | Every fulfillable item is **ready**. An order becomes ready only once every non-canceled item that remains fulfillable is ready. |
| **delivered** | Every fulfillable item is **delivered**. |
| **rejected** | Every item in the order is **rejected**. |
| **canceled** | Every item is terminal (**canceled** or **rejected**) and at least one item is **canceled**. |
| **closed** | A server closes a **delivered** order after generating its final bill. Closing is a deliberate server action and does not mean that payment was processed. |

**Closed** separates food-service completion from bill completion. An order is **delivered** when every fulfillable item has reached the guest. It becomes **closed** only when a server has generated the final bill and marks the delivered order as closed, even though payment remains outside the product scope.

## Product Principles

1. **One current operational record.** Staff should see status changes without relying on verbal handoffs or duplicate tracking.
2. **Menu accuracy at the point of browsing.** Guests should see current categories, available items, and modifiers before a server takes their order.
3. **Role-appropriate workflows.** Guests browse the menu; servers create and manage orders, confirm delivery, generate bills, and close orders; kitchen staff manage preparation and report rejection; administrators maintain the menu.
4. **Clear completion signals.** **Ready** means an item can leave the kitchen. **Delivered** means it has reached the guest. **Closed** means the server has completed billing work without implying payment was collected.
5. **Simple initial operations.** The first release prioritizes coordinated service for one restaurant rather than payments, integrations, or enterprise capabilities.

## Intended Outcome

Restaurant staff can reliably answer, at any moment, what each guest ordered, whether each item is placed, preparing, ready, delivered, canceled, or rejected, whether the order is ready, delivered, or closed, and what the tax-inclusive total is for a server-generated bill.
