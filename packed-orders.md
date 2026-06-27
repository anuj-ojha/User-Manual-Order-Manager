# Packed Orders

**Navigation:** ☰ Menu → Packed Orders  
**Route:** `/packed-orders`

---

## Overview

The Packed Orders page displays all sales orders that have been **fully packed at a fulfillment facility and are awaiting pickup by a carrier**. An order reaches this stage after all its items have been physically picked, packed into a shipment container, and marked as ready. The next step for these orders is carrier collection and shipment.

This page serves as the final fulfillment checkpoint before an order leaves the facility. Operations teams use it to track how many packed orders are staged and waiting for pickup, to identify and act on any that may need intervention, and to ship orders in bulk when ready.

The list loads automatically when the page opens and supports infinite scroll to load additional results as you scroll.

> The empty state message for this page reads: *"Orders that are packed and awaiting pickup by carrier will appear here."*

---

## Understanding the List

Each row in the Packed Orders list represents a single order. The following information is displayed per row:

| Column | Description |
|---|---|
| **Order ID** | The internal HotWax Commerce order identifier, shown in small overline text |
| **Order name / External ID** | The Shopify or external order name, along with the order's current status description |
| **Customer name** | The full name of the customer |
| **Shipping address** | The first line of the customer's shipping address. If not available, the customer ID or external ID is shown instead |
| **Address trailing line** | City, state, postal code, and country on a second line. If no city is available and the first line showed an address, this line is blank |
| **Queue reason / Rejection reason** | The reason this order is at this stage. If the order was previously rejected by a facility before being packed here, the rejection reason is shown. If no reason is available, "Reason unavailable" is displayed |
| **Rule name / Parking unit count** | The name of the routing rule that placed this order here, or, if the order has units in a parking facility, a label such as "3 units in parking" |
| **Order date** | The exact date and time the order was placed, in `MM-DD-YYYY HH:MM AM/PM` format |
| **Relative order date** | A relative label such as "Ordered 1 day ago," displayed below the exact order date |
| **Estimated delivery date** | The projected delivery date in `MM-DD-YYYY` format, derived from the order's estimated delivery date, ship-before date, or ship-by date |
| **Relative delivery label** | A relative label such as "in 2 days" indicating how soon the delivery is expected |

The results summary in the list header (e.g. "18 of 92 orders") shows how many records are currently loaded out of the total result set.

---

## Search and Filtering

A collapsible **search and filter panel** is available at the top of the page. The main search field accepts free-text queries matched against order name, order ID, and external ID.

The following additional filters are available:

| Filter | Options | Behavior |
|---|---|---|
| **Sales channel** | All sales channels / individual channels | Filters by the channel through which the order was placed |
| **Shipping method** | All methods / individual configured methods | Filters by the delivery method associated with the order |
| **Order date from** | Date picker | Shows only orders placed on or after the selected date |
| **Order date thru** | Date picker | Shows only orders placed on or before the selected date |

Clicking **Clear** resets all filters and reloads the full list.

---

## Select Mode and Bulk Actions

The Packed Orders page supports **bulk actions** to act on multiple orders simultaneously.

### Entering Select Mode

Click **"Select"** at the top right of the list header to enter Select Mode. The button label changes to **"Done"** while in this mode.

In Select Mode:
- A **checkbox** appears on the left side of each order row.
- A **"Select All"** checkbox appears in the list header to select or deselect all currently loaded orders at once.
- A footer toolbar appears at the bottom of the screen displaying the number of selected orders and available action buttons.

### Exiting Select Mode

Click **"Done"** to exit Select Mode. All selections are cleared automatically.

### Available Bulk Action

| Action | Description | Confirmation Required |
|---|---|---|
| **Ship orders** | Marks all selected packed orders as shipped, advancing them out of the packed stage. | No |

After the action completes, a brief notification (toast) appears at the top of the screen confirming the number of orders that were shipped.

---

## Navigating to an Order

In Normal Mode, clicking any order row navigates to the **Order Detail** page at the route `/orders/:orderId`.

In Select Mode, clicking a row toggles its selection instead of navigating to the order.

---

## When Does an Order Leave This List?

An order is removed from the Packed Orders list when it has been **shipped** — either through the bulk "Ship orders" action in this page, or when the carrier scans and confirms the shipment in the OMS. Once shipped, the order proceeds to a completed state.

---

*Back to [README →](../README.md)*
