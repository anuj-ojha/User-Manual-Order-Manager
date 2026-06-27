# Settings

**Navigation:** ☰ Menu → Settings  
**Route:** `/settings`

---

## Overview

The Settings page enables users to manage their personal preferences and account-level configuration for the Order Manager application. It also provides visibility into the connected OMS instance and the active product store, which are the foundational parameters that determine what data is visible throughout the application.

Changes made on the Settings page — including timezone, language, product store, and barcode identifier — take effect immediately across the application without requiring a page reload.

---

## User Profile Card

At the top of the Settings page, a card displays the **currently logged-in user's profile information**.

| Field | Description |
|---|---|
| **Avatar initials** | The user's initials, derived from their full name. If a full name is not available, the system falls back to the party ID, then the user ID, and finally displays "OM" as a default. |
| **Username** | Displayed as the subtitle on the card, showing the username, email address, or user ID (whichever is available). |
| **Full name** | Displayed as the card title, showing the user's full name or party ID. |

### Actions Available in the Profile Card

| Action | Description |
|---|---|
| **Logout** | Ends the current session. The user is redirected to the login page. |
| **Go to Launchpad** | Opens the HotWax Commerce Launchpad — the central app-switching interface — in the browser. The Launchpad URL is configured via the application's environment settings (`VITE_LAUNCHPAD_URL`). |

---

## OMS Section

This section provides information and settings related to the connected Order Management System.

### OMS Instance Card

Displays the name of the OMS instance that the application is currently connected to. This value is read from the `oms` cookie set during authentication.

If the OMS instance cannot be reached (i.e. a connectivity check to the permissions API returns no response), a red **"Offline"** badge is shown next to the instance name, alerting the user that the connection is unavailable.

An **"Go to OMS"** button is available for users with the `COMMERCEUSER_VIEW` permission. Clicking it opens the OMS administration interface in a new browser tab. This button is disabled for users who do not have this permission.

### Product Store Card

Displays a dropdown selector that allows the user to switch between **product stores** available to their account.

A product store in HotWax Commerce represents a company or a unique catalog of products. Organizations with multiple brands or multiple Shopify storefronts may have more than one product store configured. Selecting a different product store changes the scope of all order data displayed throughout the application — including order counts on the funnel, list views, and search results.

The description on the card reads: *"A store represents a company or a unique catalog of products. If your OMS is connected to multiple eCommerce stores selling different collections of products, you may have multiple Product Stores set up in HotWax Commerce."*

---

## App & Preferences Section

This section contains personal preferences that affect how the application displays and interacts with data.

### App Version Info

Displays the current version of the Order Manager application, including:
- The **version string**, derived from the build branch and revision, or the version tag.
- The **build date and time**, displayed in the user's configured timezone.

### Product Identifier

A shared component (`DxpProductIdentifier`) that allows the user to configure which **product identifiers** are used to display products throughout the application. This includes the primary identifier (used as the main label for products) and the secondary identifier (shown as supplementary information).

Supported identifier types are those configured in the OMS and may include values such as SKU, UPC, ISBN, or internal product name.

### Barcode Identifier Card

Specifies which product identifier type the application will use to **interpret barcode scans** when adding products to a manual order on the Create Order page.

The setting is labeled "Barcode Identifier." Clicking the dropdown presents a list of available good identification types sourced from the product store configuration. Selecting an identifier updates the `BARCODE_IDEN_PREF` setting for the current product store immediately.

The description on the card reads: *"Specify which product identifier should be used to scan barcodes to look up products."*

> **Tip:** The Create Order page displays a hint message if the barcode identifier is not set to SKU: *"Swap to SKU from the settings page."* SKU scanning is the most reliable mode for most workflows.

### Timezone Card

Controls the **timezone** used across the application for displaying and scheduling date and time values. The selected timezone affects the accuracy of all automated scheduling actions.

Two timezone labels are shown in this card:
- **Browser Timezone** — The timezone detected from the user's browser environment.
- **Selected Timezone** — The timezone currently saved on the user's profile.

Clicking **"Change"** opens the **Select Time Zone Modal**:

- A search bar allows you to search for any time zone by its IANA name (e.g. `America/New_York`) or its region label (e.g. `Eastern Time`).
- If the browser timezone differs from the currently selected timezone, it is listed separately at the top for quick reference.
- All filtered timezones are listed as radio options. The current time for each timezone is displayed alongside the timezone label.
- Once a timezone is selected, click the **save button** (floppy disk icon) at the bottom right of the modal to apply the change. The timezone is saved to the user's profile via the API.

The description on the card reads: *"The timezone you select is used to ensure automations you schedule are always accurate to the time you select."*

### Language Card

Allows the user to switch the application's **display language**. The currently supported languages are:

| Language | Code |
|---|---|
| English | `en-US` |
| Español (Spanish) | `es-ES` |

Selecting a language updates the application locale immediately. The choice is persisted in a cookie (`locale`) so that it is remembered on subsequent visits.

---

*Back to [README →](../README.md)*
