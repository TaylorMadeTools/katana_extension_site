---
layout: page
title: What's New
permalink: /whats-new/
---

# Discover the Latest Tools and Features

---

## Version 1.5.8 - Current Release

**Release Date:** April 17, 2026

- 🚀 **Excel File Support for Historical Imports** - Import historical sales orders from `.xlsx` and `.xls` files in addition to `.csv` — supports both native Shopify exports and template files saved as Excel
- 🔧 **Improved Date Parsing** - Robust date handling across ISO (`2025-12-03`), US (`12/03/2025`), and EU (`03/12/2025`) formats, including Excel Date objects — no more "Invalid time value" errors
- 🔧 **File Format Validation** - Unrecognized files are now rejected with a clear error instead of silently producing bad data
- 🔧 **CSV Quoted Field Handling** - RFC 4180-compliant CSV parser correctly handles commas inside quoted fields (e.g., addresses like `"123 Main St, Suite 4"`)
- 🔧 **Accurate Import Results** - Results display now shows a single consistent Succeeded/Skipped/Failed breakdown instead of contradicting counts
- � **Analytics Bug Fixes** - Minor improvements to anonymous analytics tracking and session persistence

---

## Version 1.5.7

**Release Date:** March 15, 2026

- 🔧 **Custom Field Import Fix** - Improved change detection to accept `0` as a valid field value instead of skipping it
- 🔧 **Custom Field Patch Logic** - Fields with changed values are now correctly patched even when no Collection Name is provided

---

## Version 1.5.6

**Release Date:** March 3, 2026

- 🚀 **Sales Order Multi-Field Search** - Search open sales orders by order number, customer name, address, product name, and additional info with smart rate-limit monitoring
- 🔧 **Rate Limiting & API Stability** - Fixed 429 rate-limit errors during bulk imports by consolidating API calls through centralized rate-limiting layer with automatic retries
- 🔧 **Detailed Import Progress** - Custom fields import now shows per-row progress (e.g., "Processing row 15 of 30") instead of static status messages
- 🔧 **Bulk Operations Reliability** - Improved stability for all bulk import tools (sales orders, purchase orders, custom fields) with automatic rate-limit recovery

---

## Version 1.5.5

**Release Date:** January 25, 2026

- 🚀 **Customer Order History** - View sales order history directly on customer pages with auto-load option
- 🔧 **Historical Order Import Queue** - Improved import logic and performance with queue-based processing
- 🔧 **Analytics Tracking Fixed** - Added Mixpanel tracking for customer history grid loads and multiple email tool usage
- 🔧 **Open Sales Order Import** - Fixed Row 2 deletion issue
- 🔧 **Multiple Supplier Emails** - Increased email recipient limit from 3 to 5
- 🔧 **Development Logging Improvements** - All development logs now use `console.debug()` and are commented out by default for cleaner production debugging (uncomment only when troubleshooting)

---

## Version 1.5.4

**Release Date:** December 15, 2025

- 🚀 **What's New Link** - Clicking on the version number in the extension gets you here. 😉
- 🔧 **Fixed Multi-Supplier Bugs** - 35 character category issue has been fixed 

---

## Version 1.5.3

**Release Date:** December 15, 2025

- 🚀 **New Multiple Supplier Support** - Enhanced tools to handle multiple suppliers per item with PO creation capabilities
- 🚀 **Branding Updates** - Icon Update

---

## Version 1.5.2

**Release Date:** November 12, 2025

- 🚀 **New Analytics Management Tool** - Control your data sharing preferences directly in the extension
  - Opt-in for email support and feature feedback
  - Disable analytics completely with one click

---

## Version 1.5.1

**Release Date:** November 10, 2025

- 🔒 **Analytics Improvement** - Clearer feedback on events used in the Katana Admin Panel

---

## Version 1.5.0

**Release Date:** November 7, 2025

- 🔒 **Anonymous Usage Analytics** - Help improve the extension with privacy-focused tracking (no personal data collected)
- 🚀 **Granular Tool Controls** - Show/hide individual sales tools and import features to customize your interface
- 📊 **Smarter Address Handling** - Better detection and creation of customer and supplier addresses during imports

---

## Version 1.4.2

**Release Date:** October 29, 2025

- 🔧 **Fixed Customer Import Issues** - Sales orders now correctly find and link to existing customers instead of creating duplicates

---

## Version 1.4.1

**Release Date:** October 28, 2025

- 🔧 **Fixed Detached Panel** - Restored full Historic Order Import functionality when using the extension in detached mode

---

## Version 1.4.0

**Release Date:** October 28, 2025

- 🚀 **NEW: Stock Transfer Tools** - Generate templates and import stock transfers with real-time inventory visibility
- 🚀 **NEW: Customer Reference Search** - Quickly find sales orders by customer reference number on sales pages
- 🚀 **Inventory Visibility** - See current stock levels at origin and destination locations
- 🚀 **Transfer Validation** - Visual indicators show if you have enough inventory before transferring

---

## Version 1.3.0

**Release Date:** October 26, 2025

- 🚀 **NEW: Purchase Order Discount Tool** - Apply percentage discounts to multiple purchase orders at once
- 🚀 **NEW: Sales Order Tools** - Create sales order templates and import open orders with automatic customer creation
- 🚀 **Tax Management** - Automatically find or create tax rates during sales order imports
- 🔒 **Better Data Protection** - Notes and comments are preserved when applying discounts

---

## Version 1.2.1

**Release Date:** October 14, 2025

- 🚀 **Enhanced Import Templates** - New columns for order number, created date, and fulfillment date
- 🚀 **Setup Reminders** - Quick notifications about sales tax configuration
- 🚀 **Version Display** - Extension version now displayed in the header

---

## Version 1.2.0

**Release Date:** October 2, 2025

- 🚀 **Inventory Balancing** - Automatically creates stock adjustments when importing historical sales
- 📊 **Smart Cost Calculation** - Averages costs when multiple suppliers provided the same item
- 🚀 **Faster Operations** - Improved performance for large imports
- 🚀 **Better Shopify Support** - Improved filtering and import of Shopify orders

---

## Version 1.1.0

**Release Date:** October 1, 2025

- 🚀 **Tool Visibility Management** - Now available as a standalone tool for easy access
- 🚀 **Keyboard Shortcuts** - Added Ctrl+Shift+K shortcut to quickly open the admin panel
- 🚀 **Always Accessible** - Tool management interface is always available, even when other tools are disabled

---

## Version 1.0.0 - Initial Release

**Release Date:** September 30, 2025

**Launch with 11 Powerful Tools:**

1. **Historical Sales Order Import** - Bulk import past orders with inventory balancing
2. **Sales Order Management** - Templates, import, and customer auto-creation
3. **Purchase Order Tools** - Open order templates and import capabilities
4. **Purchase Order Discounts** - Apply bulk discounts across multiple orders
5. **Customer Management** - Import, export, and bulk edit customer data
6. **Supplier Management** - Import, export, and bulk edit supplier data
7. **Service Items** - Track open service orders and manage service items
8. **Price Lists** - Efficiently assign customers to price lists
9. **Custom Fields** - Export and manage custom field data across products
10. **Multiple Emails** - Send purchase orders to multiple supplier contacts simultaneously
11. **Keyboard Shortcuts** - Quick access to common actions (Insert key for new rows)

**Core Features:**
-  Secure API key storage with encryption
-  Real-time progress tracking for all operations
-  Complete import/export functionality
-  Customizable keyboard shortcuts

---

## Version Overview

| Version | Release Date | What's New |
|---------|-------------|-----------|
| 1.5.8 | Apr 17, 2026 | Excel Import, Date Parsing & Results Display |
| 1.5.7 | Mar 15, 2026 | Custom Field Import Fix |
| 1.5.6 | Mar 3, 2026 | Sales Order Search & Rate Limiting |
| 1.5.5 | Jan 25, 2026 | Customer History & Import Queue |
| 1.5.4 | Dec 15, 2025 | What's New Link & Multi-Supplier Fix |
| 1.5.3 | Dec 15, 2025 | Multiple Supplier Support & Branding |
| 1.5.2 | Nov 12, 2025 | Analytics Management Tool |
| 1.5.1 | Nov 10, 2025 | Enhanced Import Reporting |
| 1.5.0 | Nov 7, 2025 | Analytics & Granular Tool Controls |
| 1.4.2 | Oct 29, 2025 | Customer Import Bug Fix |
| 1.4.1 | Oct 28, 2025 | Detached Panel Restoration |
| 1.4.0 | Oct 28, 2025 | Stock Transfer & Customer Search Tools |
| 1.3.0 | Oct 26, 2025 | Purchase Order & Sales Order Tools |
| 1.2.1 | Oct 14, 2025 | Enhanced Templates & Setup Reminders |
| 1.2.0 | Oct 2, 2025 | Inventory Balancing & Shopify Support |
| 1.1.0 | Oct 1, 2025 | Tool Management & Keyboard Shortcuts |
| 1.0.0 | Sep 30, 2025 | Initial Release - 11 Core Tools |

---

For detailed change information, see the [full Changelog]({{ site.baseurl }}/changelog/).
