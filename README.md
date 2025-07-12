

Dynamic EAN and Weight Display
This feature dynamically displays the EAN (Barcode) and Weight for the selected product variant on the Shopify product page. The information updates in real-time when the customer selects a different product variant.

The entire implementation is self-contained within the product.liquid file to ensure stability and bypass any theme-specific issues with external file loading.

Prerequisites: Shopify Variant Data
This feature uses standard Shopify variant properties. No custom metafields are required.

To use this feature, ensure the following fields are filled out in the Shopify Admin for each relevant product variant:

EAN (Barcode):

Navigate to a product variant.

In the Inventory section, fill in the Barcode (ISBN, UPC, GTIN, etc.) field.

Weight:

Navigate to a product variant.

In the Shipping section, ensure the This is a physical product checkbox is ticked.

Fill in the Weight field. The weight must be entered in grams. The script will automatically convert it to kilograms for display.

Implementation Details
The solution consists of a single, self-contained block of code added to the product.liquid template. This block contains four key parts:

1. Data Script
A <script> tag generates a global JavaScript object named window.productVariantData. This object is populated on the server-side using Liquid and contains a map of all variant IDs to their corresponding barcode and weight.

2. HTML Placeholders
A container <div class="product-details-extra"> with nested rows (.product-ean, .product-weight) is added to the page. These elements are hidden by default (display: none;) and act as targets for the JavaScript to inject the dynamic data.

3. CSS Styles
An embedded <style> block provides all necessary styling for the new section, including layout, typography, and borders. This ensures a consistent look and feel without relying on external or potentially non-functional Custom CSS fields.

4. JavaScript Logic
A self-contained <script>, wrapped in a DOMContentLoaded event listener, controls the feature's logic.

It defines an updateProductDetails function that finds the placeholder elements and updates their content.

It listens for the standard 'change' event on the product form.

When a variant is changed, it reads the new variant data from event.dataset.variant and calls the updateProductDetails function.

It also runs once on page load to display the details for the initially selected variant.

How to Use
Navigate to a product variant in the Shopify Admin.

In the Inventory section, enter the EAN into the Barcode field.

In the Shipping section, enter the product's weight in grams into the Weight field.

Save the variant.

The EAN and/or Weight will now automatically appear on the product page for that variant. If a field is left empty for a variant, its corresponding row will not be displayed.
