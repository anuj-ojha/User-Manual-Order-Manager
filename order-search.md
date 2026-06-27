# Find Orders

**Navigation:** ☰ Menu → Find Orders  
**Route:** `/orders`

---

## Overview

The Find Orders page is the **universal order search interface** within Order Manager. Unlike the workflow-specific pages (Open Orders, Inflight Orders, Packed Orders), which show orders in a particular stage of the fulfillment pipeline, Find Orders allows you to search across **all orders regardless of status** — including completed, cancelled, and in-progress orders.

This page is the primary tool for customer service representatives, operations managers, and any user who needs to locate a specific order by any combination of identifier, status, date range, or channel.

The search runs automatically when the page loads, showing results based on the current active product store. Results are sorted by newest order date first by default.

---

## Understanding the Results List

Each result row in the list represents a single order and displays the following information:

| Field | Description |
|---|---|
| **External ID / Order name** | Displayed as the main heading on the row (e.g. the Shopify order name such as `#1023`). Falls back to the internal order ID if no external ID is present. |
| **Internal Order ID** | Displayed on the second line alongside the customer name |
| **Customer name** | The full name of the customer, or their customer ID. Displays "Unknown customer" if neither is available. |
| **Created date label** | Shows how long ago the order was placed. For orders placed today, shows a relative label such as "Created 3h ago" or "Created less than 1h ago." For older orders, shows the date in medium format (e.g. "Created Jun 15, 2025"). |
| **Ship time left** | Displays a countdown calculated as **24 hours from the order creation time**. For example, if the order was placed 18 hours ago, it shows "in 6h." If the 24-hour window has passed, it shows "overdue." |
| **Status badge** | A colour-coded badge showing the current order status (e.g. Approved, Completed, Cancelled). |

The results summary in the list header shows the loaded count versus total results (e.g. "12 of 480 orders").

---

## Search and Filtering

A search and filter panel is available at the top of the page. The main search bar accepts free-text queries and is matched against: order name, external ID, customer name, and email. Search results update automatically after a brief 300-millisecond delay as you type.

The following additional filters are available:

| Filter | Options | Behaviour |
|---|---|---|
| **Status** | All statuses / multi-select individual statuses | A popover with checkboxes allows selecting one or more order statuses simultaneously. When "All statuses" is checked, any individual status selections are cleared. Statuses are sourced from the `ORDER_STATUS` type in the seed store. |
| **Order date from** | Date input (type="date") | Shows only orders placed on or after this date |
| **Order date thru** | Date input (type="date") | Shows only orders placed on or before this date |
| **Channel** | All channels / individual sales channels | Filters by the sales channel through which the order was placed |
| **Sort by order date** | Newest first (default) / Oldest first | Controls the sort order of results. "Newest first" uses `orderDate desc`; "Oldest first" uses `orderDate asc`. |

Changing Status, Channel, Date From, Date Thru, or Sort triggers an immediate reload. The main text search applies after the 300 ms debounce.

Clicking **Clear** resets all filters — including the search query, status selections, dates, channel, sort direction, and any custom selections — back to their defaults, and re-scopes results to the current product store.

---

## Select Mode and Bulk Actions

The **"Select" button** appears in the list header only when the logged-in user has at least one of the required permissions (`ORDER_CANCEL_PERMISSION`, `ORDER_UPDATE_PERMISSION`, or `ORDER_TASK_CREATE_PERMISSION`). If the user has none of these permissions, the Select button is not shown.

### Entering Select Mode

Click **"Select"** to enter Select Mode. The button changes to **"Done"** while in this mode.

In Select Mode:
- A **checkbox** appears on the left of each row.
- A **"Select All"** checkbox appears in the header to select or deselect all currently loaded orders.
- A footer toolbar appears at the bottom with bulk action buttons.

### Exiting Select Mode

Click **"Done"** to exit Select Mode. All selections are cleared.

### Available Bulk Actions

Each action button is shown in the footer toolbar but is **individually disabled** if the logged-in user lacks the required permission for that specific action.

| Action | Permission Required | Description | Confirmation |
|---|---|---|---|
| **Cancel open items** | `ORDER_CANCEL_PERMISSION` (`ORD_SALES_ORDER_CNCL` or `ORDERMGR_ADMIN`) | Cancels all open (unfulfilled) line items for each selected order. This action cannot be undone. | Yes — a confirmation dialog is shown before the action executes. |
| **Edit shipping method** | `ORDER_UPDATE_PERMISSION` (`ORDERMGR_UPDATE` or `ORD_SALES_ORDER_EDIT` or `ORDERMGR_ADMIN`) | Changes the shipping carrier and shipment method type for all selected orders. A modal opens to choose the new carrier and method. | No |
| **Add task** | `ORDER_TASK_CREATE_PERMISSION` (`ORD_CRT_EVENT_VIEW` or `COMM_EVNT_MENU_VIEW` or `ORDERMGR_ADMIN`) | Opens a modal to create a new order task (such as a hold or investigation) on all selected orders. | No |

After each action:
- A toast notification confirms the outcome.
- Select Mode is exited.
- For Cancel and Edit Shipping Method, the search results are refreshed.

---

## Navigating to an Order

In Normal Mode, clicking any result row navigates to the **Order Detail** page at the route `/orders/:orderId`.

In Select Mode, clicking a row toggles its checkbox selection.

---

## Infinite Scroll

When more results exist than the current loaded set, additional orders are appended automatically as you scroll to the bottom of the list.

---

*Back to [README →](../README.md)*
