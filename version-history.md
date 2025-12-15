---
layout: page
title: Version History
permalink: /changelog/
---

# Changelog

All notable changes to the Katana Master Extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

**📌 Current Version:** 1.5.3 (December 15, 2025)  
**💡 Quick Summary:** See [What's New]({{ site.baseurl }}/whats-new/) for feature highlights for each release.

## [Unreleased]

### Planned
- Additional keyboard shortcuts beyond Insert key  
- New tools based on user feedback and Katana page requirements
- Advanced export/import capabilities
- Integration with additional Katana API endpoints

## [1.5.3] - 2025-12-15

### Added

- **🚀 NEW: Multiple Supplier Support** - Enhanced tools and workflows to handle multiple suppliers
  - Improved supplier management across import and export operations
  - Better integration with multi-supplier scenarios
  - Enhanced flexibility for complex supplier workflows

### Changed

- **🎨 Branding Updates** - Refreshed visual design and interface consistency
  - Updated color schemes and visual elements
  - Improved UI consistency throughout the extension
  - Enhanced overall aesthetic and user experience
- **Interface Refinement** - Improved user experience across all tools
  - Better visual hierarchy and layout consistency
  - Streamlined interface for improved usability

### Fixed

- **Supplier Workflow Improvements** - Better handling of multiple supplier scenarios
  - Improved data accuracy in multi-supplier contexts
  - Enhanced validation and error handling

## [1.5.2] - 2025-11-12

### Added

- **🚀 NEW: Analytics Opt-In Management Tool** - Complete user control over analytics preferences
  - Email opt-in for direct support and feature feedback with instant setup
  - "Disable All Analytics" option with confirmation dialog for complete privacy control
  - Re-enable analytics option for users who change their mind
  - Real-time status display showing current analytics and email preferences
- **Enhanced Privacy Controls** - Self-service analytics management without contacting support
  - One-click opt-out from all analytics tracking with user confirmation
  - Seamless integration between analytics preferences and MixpanelAPI tracking
  - Persistent local storage of all privacy preferences with instant application

### Changed

- **Unified Client ID Management** - Eliminated duplicate ID generation between analytics and tracking systems
  - Single source of truth for client ID generation through MixpanelAPI class
  - Consistent "client\_" prefix across all anonymous tracking maintaining reporting continuity
  - Analytics opt-in tool now reads actual MixpanelAPI client ID instead of generating separate IDs
- **Enhanced User Experience** - Streamlined analytics preferences interface
  - Clear visual feedback for all three analytics states (anonymous, opted-in, disabled)
  - Instant UI updates when preferences change without requiring page refresh
  - Comprehensive status display showing current user ID and preference state

### Fixed

- **Client ID Consistency Issues** - Resolved redundant ID generation causing analytics fragmentation
  - Removed duplicate generateRandomUserId() function from analyticsOptIn.js
  - Fixed inconsistent client ID usage between tracking and display systems
  - Ensured single client ID used across extension for accurate analytics tracking

### Security

- **Enhanced Privacy Compliance** - Complete user control over all data collection
  - Anonymous analytics can be completely disabled with single click
  - No tracking occurs when analytics is disabled - MixpanelAPI returns early from all events
  - Clear confirmation dialog explaining benefits of anonymous data before opt-out
  - All privacy preferences stored locally with no external transmission

## [1.5.1] - 2025-11-10

### Fixed

- **🔧 Development File Loading** - Eliminated console errors for missing development files
  - Silent fallback for missing key.json and key.txt files in production environments
  - Generate random user ID for analytics when no development keys are present
  - Improved production stability by removing unnecessary error logging for dev-only files
- **📊 Analytics Restoration** - Restored "Admin Panel Opened" session tracking
  - Re-implemented session_start analytics event that was accidentally removed
  - Ensures consistent analytics collection for panel usage metrics
- **📈 Enhanced Import Analytics** - Added detailed metrics for import operations
  - Line item count tracking for sales order and purchase order imports
  - Total quantity metrics for imported orders providing volume insights
  - Enhanced analytics granularity for better usage pattern understanding

## [1.5.0] - 2025-11-07

### Added

- **🚀 NEW: Anonymous Usage Analytics** - Privacy-focused analytics system for extension improvement
  - Anonymous usage tracking for tool usage patterns and success/failure rates
  - No personal data, Order IDs, Customer IDs, or any Katana identifiers collected
  - Aggregate statistics only: operation counts, error rates, tool popularity
  - Optional analytics help improve tool reliability and guide development priorities
- **Enhanced Sales Tools Granular Control** - Individual component visibility management
  - Historical Sales Order Import component can be individually controlled (hidden by default)
  - Sales Order Template & Import buttons can be controlled separately
  - Sales Order Search Box can be controlled independently
  - Improved user customization of sales interface reducing clutter
- **Enhanced Import Success Messages** - Comprehensive operation reporting
  - Customer import results now show separate counts for customers and addresses created/updated
  - Supplier import results now show separate counts for suppliers and addresses created/updated
  - Better visibility into all operations performed during import processes
- **Improved Address Creation Logic** - Enhanced supplier/customer address handling
  - Fixed address creation when Address ID is blank but address data is provided
  - Automatic address creation for existing suppliers/customers when new address data is added
  - Better detection of address data presence for create vs update decisions

### Changed

- **Mixpanel Integration Architecture** - Implemented privacy-first analytics framework
  - ES6 module compatibility with global window assignment for broad tool support
  - Centralized analytics API with consistent event structure across all tools
  - Automatic development vs production environment detection and filtering
- **Tool Visibility System Enhancement** - Extended granular control to sales tools
  - Sales tools broken down into 3 individually controllable components
  - Historical Import hidden by default to reduce interface complexity
  - Conditional event listener attachment only for visible components
- **Import Result Display Improvements** - Enhanced feedback and transparency
  - Detailed breakdown showing customers/suppliers created vs updated separately
  - Address operations clearly reported alongside main entity operations
  - Global info box messages include address operation counts when applicable

### Fixed

- **🚨 CRITICAL: Supplier Address Creation Bug** - Fixed addresses not being created when Address ID was blank
  - Added logic to detect address data presence when no Address ID exists
  - Proper address creation triggering for suppliers with new address information
  - Consistent address handling between update and create scenarios
- **Mixpanel Export Compatibility Issues** - Resolved ES6 module import conflicts
  - Fixed "does not provide an export named 'default'" errors in customer/supplier tools
  - Changed from ES6 imports to global window object access for compatibility
  - Resolved syntax errors when mixpanel-api.js loaded as regular script vs module
- **Keyboard Shortcuts Analytics** - Added tracking for shortcut configuration changes
  - "Add new row shortcut used" event with success indicator and selected key
  - Enhanced debugging and usage pattern understanding

### Security

- **Privacy-First Analytics Implementation** - Zero personal data collection
  - Explicit exclusion of all Katana IDs (Order IDs, Customer IDs, Purchase Order IDs, etc.)
  - Only aggregate counts, percentages, success/failure indicators collected
  - No personally identifiable information transmitted to analytics service
  - Full compliance with privacy policy and user data protection standards

## [1.4.2] - 2025-10-29

### Fixed

- **🚨 CRITICAL: Sales Order Customer Duplication Bug** - Fixed critical issue where sales order imports were creating duplicate customers instead of finding existing ones
- **Customer Data Structure Handling** - Corrected improper handling of fetchAllCustomers API response structure in both salesTools.js and historicalSalesOrders.js
- **Customer Lookup Logic** - Enhanced customer search functionality with proper data extraction from API response wrapper
- **Import Data Integrity** - Sales order imports now correctly identify existing customers by email, preventing unnecessary customer creation

### Changed

- **Enhanced Debug Logging** - Added comprehensive debugging for customer search process showing loaded customer count and search results
- **Improved API Response Handling** - Better handling of both direct array and wrapped response formats from fetchAllCustomers function
- **Customer Search Robustness** - More reliable customer lookup with fallback mechanisms and detailed progress reporting

## [1.4.1] - 2025-10-28

### Fixed

- Fixed Historic Order Import (HSI) detached panel functionality that was broken in previous version
- Restored missing historicalSalesOrders.js file from version control
- Resolved issue where HSI detached panel only displayed "Logs" instead of full import interface

## [1.4.0] - 2025-10-28

### Added

- **🚀 NEW: Stock Transfer Management Tools** - Complete stock transfer template generation and import system
  - Excel template generation with locations dropdown validation and inventory lookup formulas
  - Real-time inventory visibility showing current stock levels at origin and destination locations
  - Advanced validation with conflict detection for transfer-level fields (locations, dates)
  - Auto-population feature for efficient multi-line transfer entry
  - Comprehensive validation rules with visual indicators (green for sufficient stock, red for conflicts)
  - Support for both /stocktransfers and /stocktransfers/done pages
- **🚀 NEW: Customer Reference Search** - Quick sales order lookup by customer reference number
  - Instant search functionality on sales pages for finding orders by customer reference
  - Real-time results display with clickable order links in History box
  - Integration with existing sales tools for seamless workflow
  - Search results persist in Memory box with clear success/error messaging
- **Enhanced Sidepanel Width Management** - Improved responsive design and width control
  - Enhanced CSS layout ensuring header and footer expand properly with sidepanel width
  - Improved responsive behavior maintaining usability across different panel sizes

### Changed

- **Display Tools Architecture** - Added stock transfer tools to tool visibility management system
- **Sales Tools Integration** - Enhanced sales tools with customer reference search functionality
- **Tool Registry Expansion** - Updated tool registry to include stock transfer tools for /stocktransfers URLs
- **CSS Layout Improvements** - Enhanced flexbox layout for better responsive behavior across all components

### Fixed

- **Header/Footer Width Issues** - Fixed header and footer not expanding to full width when sidepanel is resized
- **Layout Responsiveness** - Improved overall layout behavior ensuring all elements scale properly together
- **Tool Loading Logic** - Enhanced tool ID mapping to properly handle stock transfer page URLs

### Security

- **Consistent API Integration** - Stock transfer tools follow established security patterns for API key handling and data validation

## [1.3.0] - 2025-10-26

### Added
- **🚀 NEW: Purchase Order Discount Tool** - Complete bulk discount application system for purchase order management
  - Apply percentage discounts to all pending (non-received) purchase order rows
  - Automatic Purchase Order ID extraction from URLs
  - Smart filtering to protect received items from modification
  - Real-time progress tracking with detailed status updates
  - Comprehensive error handling and debugging capabilities
- **🚀 NEW: Sales Order Management Tools** - Unified interface for open sales order template generation and import
  - Excel template generation with built-in validation rules and help worksheets
  - Complete sales order import with customer auto-creation and SKU-to-variant mapping
  - Tax rate find/create functionality with proper percentage-to-basis-points conversion
  - Comprehensive import process with detailed success/error reporting
- **Purchase Order API Enhancement** - Added `getPurchaseOrder()` function to purchaseOrders.js API module for retrieving individual purchase order details
- **Enhanced Note Preservation** - Purchase Order Discount Tool retrieves existing additional_info before updating to preserve audit trails
- **Smart Note Appending** - Discount notes are prepended to existing purchase order notes with proper formatting and timestamps

### Changed
- **Sales Tools Architecture** - Unified sales tools into comprehensive management interface combining historical and open order functionality
- **Purchase Order Discount Workflow** - Enhanced workflow: retrieve existing PO → apply discounts → append notes → update PO with complete data preservation
- **API Integration** - Improved integration between discount tool and purchase order retrieval for comprehensive data handling
- **Template System** - Enhanced Excel template generation with validation rules, help worksheets, and example data

### Fixed
- **🚨 CRITICAL: Purchase Order Note Overwriting** - Fixed issue where applying discounts would completely overwrite existing purchase order additional_info notes
- **Note Formatting Logic** - Improved note concatenation with double newline separator (`\n\n`) for better readability between discount and existing content
- **Data Preservation** - Purchase order discount tool now maintains complete audit trail by preserving all existing notes when adding discount information

### Security
- **Data Integrity** - Enhanced data preservation prevents accidental loss of important purchase order notes during discount application
- **Import Validation** - Comprehensive validation of sales order import data before processing to prevent data corruption

## [1.2.1] - 2025-10-14

### Added
- **Enhanced Historical Sales Orders Template** - Added order_number, created_date, and fulfillment_date as first three columns for better order tracking
- **Sales Tax Configuration Notice** - Added informational notice about default sales tax application during historical imports with quick access to tax settings
- **Version Display in Header** - Dynamic version display in sidepanel header automatically synced with manifest.json version
- **Enhanced Template Column Support** - Added missing business-critical columns (billing_company, shipping_company, shipping_phone, ecommerce_order_id) to template processing

### Fixed
- **🚨 CRITICAL: CSV Template Format Detection** - Fixed major bug where enhanced CSV templates were incorrectly detected as Shopify exports, preventing template imports
- **CSV Header Parsing Logic** - Corrected flawed header detection that caused template files to use hardcoded Shopify headers instead of actual template headers
- **Shopify Store URL Section Visibility** - Fixed issue where Shopify store name input appeared for non-Shopify template files
- **Template Format Priority Detection** - Improved format detection to properly identify template formats before falling back to Shopify detection
- **CSV Parsing Robustness** - Enhanced CSV parser to handle template headers correctly and avoid false positive Shopify format detection

### Changed
- **Improved Format Detection Logic** - More restrictive and accurate detection between template and Shopify formats with priority checking for template indicators
- **Enhanced Debug Output** - Added comprehensive debugging showing raw CSV content, detected headers, and format detection reasoning
- **Template Processing Backward Compatibility** - Maintained support for both old and new template formats while adding enhanced columns

### Security
- **Robust CSV Parsing** - Improved CSV parsing security to handle various file formats and prevent format confusion attacks

## [1.2.0] - 2025-10-02

### Added
- **Inventory Balancing System** - Automatic stock adjustment creation to balance historical sales (Stock Added = Stock Sold principle)
- **Cost Averaging Logic** - Averages unit costs per SKU when multiple costs are provided in import data

### Changed
- **Rate limiting delay** - 1.5 second → 1 second delay between calls
- **Improved Shopify Column Mapping** - Changed from "Fulfillment Status" to "Lineitem fulfillment status" for more accurate order filtering
- **Fulfillment-Only Import Logic** - Shopify imports now process only fulfilled orders, skipping unfulfilled orders entirely to maintain inventory accuracy
- **Multi-Phase Import Process** - Structured import workflow: Stock Adjustments → Customers → Sales Orders → Fulfillments
- **Real-time Progress Tracking** - Enhanced progress system with per-phase updates and detailed status reporting

### Fixed
- **Status Field Mapping** - Corrected Shopify status field mapping to use proper column references
- **Template Format Filtering** - Removed inappropriate status filtering from template format imports
- **Cost Handling Logic** - Improved cost per unit calculation with proper averaging and fallback to $0.00 when no costs provided
- **Comprehensive Error Handling** - Enhanced error reporting with specific per-row status tracking and downloadable results logs

### Security
- **Data Integrity Checks** - Comprehensive validation of historical order data before processing

## [1.1.0] - 2025-10-01

### Added
- **🔒 Lockout Prevention System** - Display Tools interface is now always accessible on settings pages to prevent users from being locked out when all tools are disabled
- **Independent Tool Architecture** - Separated Display Tools from Keyboard Shortcuts for better modularity and reliability
- **Enhanced Tool Visibility Management** - Display Tools now show "ALWAYS ON" status to indicate they cannot be disabled

### Changed
- **Improved Settings Page Architecture** - Display Tools and Keyboard Shortcuts now load independently, allowing keyboard shortcuts to be disabled without affecting tool management
- **Better Tool Loading Logic** - Enhanced tool registration system with proper separation of concerns between display management and individual tool functionality
- **Streamlined Event Handling** - Simplified event attachment with improved timing and reliability

### Fixed
- **🚨 CRITICAL: CSP Violation** - Removed inline event handlers (`onmouseover`, `onmouseout`) from sidepanel.html that were causing Content Security Policy errors
- **Tool Management Lockout** - Fixed issue where disabling all tools would hide the Display Tools interface, preventing users from re-enabling tools
- **Event Handler Timing** - Resolved DOM timing issues with event attachment using `requestAnimationFrame` for proper sequencing
- **Tool Visibility Logic** - Corrected tool loading behavior to ensure Display Tools are always available regardless of other tool settings

### Security
- **Content Security Policy Compliance** - Replaced inline JavaScript event handlers with CSS-only hover effects to meet CSP requirements
- **Enhanced Extension Security** - Improved event handling patterns following Chrome extension security best practices

## [1.0.0] - 2025-09-30

### Added
- **🎉 INITIAL CHROME WEB STORE RELEASE** - Production-ready extension with comprehensive functionality
- **12 comprehensive tools** for Katana MRP workflow enhancement:
  1. Price List Customer Template & Import Tool
  2. Service Item Open Orders Tool  
  3. Customer Data Management (with edit functionality)
  4. Supplier Data Management (with edit functionality)
  5. Data Table Component
  6. Custom Field Tools (unified across Products, Materials, Inventory)
  7. Service Items Management Tool
  8. Keyboard Shortcuts Tool
  9. Tool Visibility Management System
  10. Multiple Email Tool (Purchase Orders)
  11. Purchase Order Discount Tool
  12. Sales Order Management Tools
- **Centralized API architecture** with 9 specialized modules eliminating code duplication
- **Progress tracking system** with real-time feedback replacing all loading wheels
- **Encrypted API key storage** with AES-GCM encryption and session-based security
- **Tool visibility management** with persistent settings and collapsible interface
- **Keyboard shortcuts system** with Insert key for "Add New Row" and Ctrl+Shift+K for admin panel
- **Data table component** with multi-format input, export capabilities, and optional editing
- **Service import/export** with hash-based change detection and dual create/update modes
- **Hash-based change detection** for efficient updates across customer, supplier, and service tools

### Changed
- **Consolidated custom field tools** from three separate tools into single unified interface
- **Migrated from loading wheels** to modern progress system with real-time feedback
- **Improved user interface** with collapsible tool management reducing complexity
- **Enhanced error handling** and debugging capabilities across all tools
- **Streamlined tool loading** with proper debouncing and visibility management

### Fixed
- **Individual fulfillment progress logging** in historical sales orders tool
- **Tool loading and duplication issues** with proper state management
- **Import path errors** across multiple tools for reliable module loading

## Key Features by Tool

### Customer Data Management
- **Download:** Export all customer data with proper formatting
- **Import:** Bulk customer creation from Excel templates
- **Edit:** Update existing customers with hash-based change detection
- **Validation:** Comprehensive data validation and error reporting

### Supplier Data Management  
- **Download:** Complete supplier export including contact information
- **Import:** Bulk supplier creation with template support
- **Edit:** Update supplier data with change detection
- **Multiple Emails:** Support for multiple email addresses per supplier (Purchase Order tool)

### Service Items Management
- **Export:** Download all service items with complete details
- **Import:** Create new service items from templates
- **Update:** Modify existing services with hash detection
- **Order Tracking:** View open orders for individual service items

### Custom Field Tools
- **Products Export:** Download products with custom field values
- **Materials Export:** Export materials including custom fields
- **Inventory Export:** Complete inventory data with custom fields
- **Bulk Editing:** Modify custom field values in bulk operations

### Multiple Email Tool (Purchase Orders)
- **Automatic Detection:** Identifies suppliers with multiple configured emails
- **Background Processing:** Runs automatically without user intervention
- **Error Handling:** Graceful processing of email validation errors
- **Multi-Recipient Support:** Sends to up to 3 email addresses per supplier

**⚠️ Important Notes:**
- Multiple emails may impact QuickBooks Online integration
- Suppliers with multiple emails show validation errors in Katana UI
- Future edits require Admin Panel or extension tools

### Tool Visibility Management
- **Page-Specific Controls:** Show/hide tools per page type
- **Persistent Settings:** Preferences saved across sessions
- **Collapsible Interface:** Reduces UI complexity when needed
- **Real-time Updates:** Changes apply immediately without refresh

### Keyboard Shortcuts
- **Insert Key:** Automatically clicks "Add New Row" buttons
- **Ctrl+Shift+K:** Opens Katana admin panel in new tab
- **Context Aware:** Only activates on appropriate pages
- **Configurable:** Enable/disable shortcuts as needed

## Technical Improvements

### API Architecture
- **Centralized System:** All API calls through unified system
- **Error Handling:** Consistent error processing across tools
- **Authentication:** Centralized API key management
- **Modularity:** Reusable API methods reduce code duplication

### Progress Tracking
- **Real-time Updates:** Live progress bars for all operations
- **Detailed Logging:** Comprehensive operation history
- **Error Reporting:** Clear error messages with solutions
- **Result Downloads:** Detailed result files for review

### Security Enhancements
- **Encrypted Storage:** AES-GCM encryption for API keys
- **Session-Based:** Keys cleared on browser close
- **Local Only:** No data transmitted to third parties
- **Direct API:** All requests go directly to Katana servers

---

**For detailed usage instructions, see the [User Guide]({{ site.baseurl }}/instructions/)**

**For technical details, see the [Technical Documentation]({{ site.baseurl }}/readme/)**