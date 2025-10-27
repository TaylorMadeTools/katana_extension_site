---
layout: page
title: Technical Documentation
permalink: /readme/
---

# How does it work?

> **👋 New User?** Check out [**User Guide**]({{ site.baseurl }}/instructions/) for simple, step-by-step guides on using each tool.
>
> **🔧 Developer/Technical User?** You're in the right place! This page contains complete technical documentation.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Current Tools](#current-tools)
- [API Architecture](#api-architecture)
- [Debug Panel](#debug-panel)
- [Hash Tool: Why and How We Use It](#hash-tool-why-and-how-we-use-it)
- [Security](#security)
- [Usage Notes](#usage-notes)
- [Future Tools](#future-tools)

## Overview

This Chrome extension enhances the Katana MRP web experience by providing advanced tools and workflow automation directly in a persistent side panel. It is designed for use with https://factory.katanamrp.com and interacts with the Katana API using your personal API key.

## Features

### API Key Entry and Storage
- Secure local storage of your Katana API key
- Automatic validation and error handling
- Session-based storage for security

### Navigation and Tool Loading
- Context-aware tool loading based on current Katana page
- Dynamic side panel that appears on relevant pages
- Smooth navigation between different tool sets

### Global History Info Box
- Persistent activity log across all tools
- Real-time progress tracking
- Detailed operation results and error reporting

### Keyboard Shortcuts
- **Ctrl+Shift+K** → Opens Katana admin panel in new tab
- **Insert key** → Clicks "Add New Row" buttons (configurable)
- Customizable shortcuts for power users

## Current Tools

### 1. Price List Customer Template & Import Tool
**Location:** Price Lists pages  
**Purpose:** Bulk assignment of customers to price lists

**Features:**
- Download customer template with price list dropdowns
- Bulk import with duplicate detection
- Progress tracking and result reporting

### 2. Service Item Open Orders Tool
**Location:** Individual service item pages  
**Purpose:** View all open sales orders for a specific service

**Features:**
- Real-time order lookup via API
- Clickable order numbers that open in new tabs
- Results accumulated in memory for comparison

### 3. Customers Tool (with Edit Functionality)
**Location:** Customer pages  
**Purpose:** Comprehensive customer data management

**Features:**
- **Download:** Export all customer data to Excel
- **Import:** Add new customers from spreadsheet
- **Edit:** Bulk update existing customer information
- **Validation:** Built-in data validation and error handling
- **Hash-based change detection** for efficient updates

### 4. Suppliers Tool (with Edit Functionality)
**Location:** Supplier pages  
**Purpose:** Complete supplier data management

**Features:**
- **Download:** Export supplier data with all fields
- **Import:** Bulk supplier creation
- **Edit:** Update existing supplier information
- **Multiple email support** for purchase order automation
- **Hash-based change detection**

### 5. Data Table Component
**Purpose:** Reusable component for displaying and managing data

**Features:**
- Sortable columns
- Filterable data
- Pagination support
- Export functionality
- Responsive design

### 6. Custom Field Tools (Unified)
**Location:** Products, Materials, Inventory pages  
**Purpose:** Export and manage custom field data

**Features:**
- Export products/materials with custom field values
- Bulk editing of custom field collections
- Support for all custom field types
- Excel-formatted output

### 7. Service Items Management Tool
**Location:** Services pages  
**Purpose:** Bulk service item operations

**Features:**
- Export existing service items
- Import new service items
- Update existing services
- Template generation

### 8. Keyboard Shortcuts Tool
**Purpose:** Enhanced keyboard navigation

**Features:**
- Insert key automation for "Add New Row" buttons
- Configurable shortcut management
- Context-aware activation

### 9. Tool Visibility Management
**Location:** Settings page  
**Purpose:** Control which tools appear on each page type

**Features:**
- Granular visibility controls
- Per-page-type configuration
- Real-time updates without refresh

### 10. Multiple Email Tool (Purchase Orders)
**Location:** Purchase Order pages  
**Purpose:** Send POs to multiple supplier contacts automatically

**Features:**
- **Automatic detection** of suppliers with multiple emails
- **Background processing** - no manual activation required
- **Error handling** for email validation issues
- **Support for up to 3 emails** per supplier

**⚠️ Important Considerations:**
- **QBO Integration:** Multiple emails may cause QuickBooks Online sync issues
- **Supplier Editing:** Suppliers with multiple emails show validation errors in Katana UI
- **Admin Panel Required:** Future supplier edits must use Admin Panel or this tool

### 11. Purchase Order Discount Tool
**Location:** Purchase Order pages  
**Purpose:** Apply bulk percentage discounts to purchase order items

**Features:**
- **Automatic PO ID detection** from URL for seamless operation
- **Smart item filtering** - only affects pending (non-received) items
- **Note preservation** - maintains existing purchase order notes
- **Real-time progress tracking** with detailed status updates
- **Comprehensive error handling** and debugging capabilities
- **Audit trail maintenance** - appends discount information to existing notes

**Safety Features:**
- **Received item protection** - automatically skips items already received
- **Data integrity** - preserves all existing purchase order information
- **Timestamped logging** - tracks all discount applications with timestamps

### 12. Sales Order Management Tools
**Location:** Sales pages  
**Purpose:** Comprehensive sales order template generation and bulk import

**Features:**
- **Excel template generation** with built-in validation rules and help worksheets
- **Customer auto-creation** - automatically creates new customers during import
- **SKU-to-variant mapping** - seamless product variant handling
- **Tax rate management** - finds existing rates or creates new ones
- **Multi-phase import process** - customers → orders → line items → tax processing
- **Comprehensive validation** - prevents data corruption with thorough checks
- **Detailed result reporting** - downloadable success/error logs

**Technical Capabilities:**
- **Percentage-to-basis-points conversion** for tax rate compatibility
- **Duplicate detection** and handling during customer creation
- **Variant resolution** from product SKUs for accurate inventory tracking
- **Error recovery** - detailed error messages for issue resolution

## API Architecture

### Centralized API Layer ✅ Completed
All API interactions are now managed through a centralized system located in `src/tools/api/`.

### API Modules (`src/tools/api/`)
- **`factory.js`** - Core API client with authentication and base methods
- **`customers.js`** - Customer-specific API operations
- **`suppliers.js`** - Supplier-specific API operations  
- **`services.js`** - Service item API operations
- **`priceLists.js`** - Price list API operations
- **`customFields.js`** - Custom field API operations
- **`purchaseOrders.js`** - Purchase order operations and discount management
- **`salesOrders.js`** - Sales order creation and management operations
- **`products.js`** - Product API operations and management
- **`materials.js`** - Materials API operations and management
- **`variants.js`** - Product variant API operations
- **`inventory.js`** - Inventory management API operations
- **`locations.js`** - Location/warehouse API operations
- **`stockAdjustments.js`** - Stock adjustment API operations
- **`tax.js`** - Tax rate management API operations

### Utility Layer (`src/tools/utils/`)
- **`apiHelpers.js`** - Common API utility functions and helpers
- **`progressComponents.js`** - Progress bar and status management components

### Benefits
- **Consistent error handling** across all tools
- **Centralized authentication** management
- **Reusable API methods** reduce code duplication
- **Standardized data processing** pipeline
- **Unified progress tracking** system

### Usage Pattern
```javascript
// Example API usage
import { customers } from '../api/customers.js';
import { progressComponents } from '../utils/progressComponents.js';

async function importCustomers(data) {
    const progressBar = progressComponents.create('Importing customers');
    
    try {
        const result = await customers.bulkImport(data, {
            onProgress: progressBar.update,
            validate: true
        });
        
        progressBar.complete('Import successful');
        return result;
    } catch (error) {
        progressBar.error(`Import failed: ${error.message}`);
        throw error;
    }
}
```

## Debug Panel

The debug panel provides technical information for troubleshooting:

- **API request/response logging**
- **Performance metrics**
- **Error stack traces**
- **Memory usage statistics**
- **Tool activation history**

Access via the toggle button in the extension footer.

## Hash Tool: Why and How We Use It

### What is the Hash Tool?
The hash tool generates unique fingerprints for data records, enabling efficient change detection during bulk edit operations.

### Why Use Hashes?
1. **Performance:** Only process records that have actually changed
2. **Safety:** Detect accidental modifications to critical data
3. **Audit Trail:** Track what changes were made and when
4. **Bandwidth:** Reduce API calls by skipping unchanged records

### Example Workflow
1. **Export:** Download customer data with hash columns
2. **Edit:** Make changes to customer information
3. **Import:** Tool compares new hashes with original hashes
4. **Process:** Only modified records are sent to the API

### Technical Example: How Hashes Are Computed
```javascript
// Simplified hash generation
function generateRecordHash(record) {
    const hashableFields = ['displayName', 'email', 'address', 'phone'];
    const hashString = hashableFields
        .map(field => record[field] || '')
        .join('|');
    return btoa(hashString).slice(0, 16); // Base64 encoded, truncated
}
```

## How to Use Edit Functionality (Customers & Suppliers)

### For Existing Records
1. **Export current data** using the download button
2. **Modify data** in the Excel file (don't change ID or hash columns)
3. **Re-import** the modified file
4. **Review results** - only changed records are processed

### For New Records  
1. **Download a template** or existing data
2. **Add new records** with blank ID fields
3. **Import** - new records are created, existing ones updated based on changes

### Critical Rules
- **Never modify** Customer ID or Hash columns
- **Always validate** email addresses and required fields
- **Test with small batches** before bulk operations
- **Review result files** to confirm successful operations

## Security

- **Local Storage Only:** API keys stored locally in browser
- **No Data Transmission:** No data sent to third-party servers
- **Katana API Direct:** All requests go directly to Katana's servers
- **Session-Based:** API keys cleared on browser close
- **Encrypted Storage:** Browser's built-in encryption for stored data

## Usage Notes

- **API Key Required:** Get yours from Katana Settings → Integrations → API
- **Active Session:** Must be logged into Katana for tools to work
- **Page Context:** Tools appear automatically based on current page
- **Progress Tracking:** Watch the progress bars for real-time status
- **Result Downloads:** Many tools provide detailed result files
- **Error Handling:** Clear error messages with suggested solutions

## Future Tools

Planned enhancements include:

- **Purchase Order Management** - Bulk PO operations
- **Sales Order Tools** - SO creation and management
- **Inventory Adjustments** - Bulk inventory updates  
- **Recipe Management** - Import/export product recipes
- **Advanced Reporting** - Custom report generation
- **Workflow Automation** - Multi-step process automation
- **Integration Hub** - Connect with external systems

---

**Need step-by-step instructions?** Check out the [User Guide]({{ site.baseurl }}/instructions/) for detailed, non-technical instructions on using each tool.