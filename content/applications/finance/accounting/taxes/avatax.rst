==================
AvaTax integration
==================

Avalara's *AvaTax* is a cloud-based tax software that delivers the latest sales and use
tax calculations to Odoo's sales and invoicing flow when the customer makes a purchase. *AvaTax* tax
calculation is supported in every United Nations charted country. This includes inter-boarder
transactions as well.

.. important::
   Use of AvaTax for your company is only available for companies with locations in the United
   States and Canada.

*AvaTax* accounts for location-based tax rates for each state, county and city. It improves
remittance accuracy by paying close attention to laws, rules, jurisdiction boundaries, and special
circumstances like tax holidays and product exemptions. Companies who integrate with *AvaTax* can
maintain control of tax-calculations in-house with this simple :abbr:`API (application programming
interface)` integration.

Avalara provides the following services:

- AvaTax (sales and use tax calculations)
- Avalara returns (prepare, file, and remit sales tax returns)
- Avalara Exemption Certificate Management (collect, store, and manage documents)
- Avalara tax Research (Get tax research in plain language)
- Avalara Business License Services (project based assistance to help confront challenges to their
  license operations)

.. important::
   Some limitations exist in Odoo while using AvaTax for tax calculation:

   Point of Sale is not supported but it most cases a dynamic tax calculation model (like AvaTax) is
   not necessary because the delivery address is always static, the store or restaurant itself.

   AvaTax and Odoo use the company address and not the warehouse address.

   Exercise tax is not supported. This includes tabacco/vape taxes, fuel taxes, and other specific
   industries.

.. seealso::
   Avalara's support documents: `About AvaTax
   <https://community.avalara.com/support/s/document-item?language=en_US&bundleId=dqa1657870670369_dqa1657870670369&topicId=About_AvaTax.html&_LANG=enus>`_

To use *AvaTax*, an account with Avalara is required for the setup. If one has not been set up yet,
connect with Avalara to purchase a license: `Avalara: Let's Talk
<https://www.avalara.com/us/en/get-started.html>`_

.. important::
   Upon account setup, take note of the AvaTax :guilabel:`Account ID`. This will be needed in the
   :ref:`Odoo setup <avatax/credentials>`. In Odoo this number is the :guilabel:`API ID`.

Set up on AvaTax (onboarding)
=============================

 First `create a basic company profile
 <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Create_a_Basic_company_profile.html&_LANG=enus>`_.

Create basic company profile
----------------------------

Gather some key information about the business. Things that are necessary for the next step are:
where the company collects tax, products and service that the company sells and where each is sold,
and finally which customer are exempt from tax, if any.

Follow the Avalara documentation for creating a basic company profile:

#. `Add your company information
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_your_company_information.html&_LANG=enus>`_.
#. `Tell us where you collect and pay tax
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Tell_us_where_you_collect_and_pay_tax.html&_LANG=enus>`_.
#. `Verify your jurisdictions and activate your company
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Verify_your_jurisdictions_and_activate_your_company.html&_LANG=enus>`_.
#. `Add other company locations for location-based filing
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_other_company_locations_for_location-based_filing.html&_LANG=enus>`_.
#. `Add a marketplace to your company profile
   <https://community.avalara.com/support/s/document-item?bundleId=dqa1657870670369_dqa1657870670369&topicId=Add_marketplace_transactions_to_your_company_profile.html&_LANG=enus>`_.

.. _avatax/create_avalara_credentials:

Connect to AvaTax
=================

Following creating the basic company profile in Avalara, a connection to AvaTax **must** be made.
This step is necessary to connect Odoo to AvaTax and vice-versa.

Navigate to either Avalara's `sandbox <https://sandbox.admin.avalara.com/>`_ or `production
<https://admin.avalara.com/>`_ environment. This will depend on which type of Avalara account the
company would like to integrate.

.. seealso::
   Avalara's documentation on `sandbox vs production environments
   <https://knowledge.avalara.com/bundle/fzc1692293626742/page/sandbox-vs-production.html>`_.

Login to create the :guilabel:`Licence Key`. Go to :menuselection:`Settings --> License and API
Keys`. Click :guilabel:`Generate Licence Key`.

A warning will display stating: `If your business app is connected to Avalara solutions, the
connection will be broken until you update the app with the new license key. This action cannot be
undone.`

Should this be the first :abbr:`API (application programming interface)` integration being
made with AvaTax and Odoo, then click :guilabel:`Generate license key`.

Should this be an additional license key then, ensure the previous connection can be broken. There
is **only** one license key associated with each of the Avalara sandbox and production accounts.

Copy this key to a safe place. It is strongly encouraged to *download*, *print*, *copy and paste*,
or *write* down the license key for future reference. This key is un-retrievable after leaving this
screen.

Configuration in Odoo
=====================

Before using AvaTax there are some additional configurations in Odoo to ensure tax calculations are
made accurately.

Ensure that the company has data set up in the Odoo database. When the database or company is
initially set up, a country is set. This country sets the fiscal position and helps *AvaTax*
calculate the correct tax rates.

.. seealso::
   Refer to this documentation for more information: :doc:`../../fiscal_localizations`.

Fiscal Country
--------------

First, ensure that the :guilabel:`Fiscal Country` is set. To set it, navigate to,
:menuselection:`Accounting --> Configuration --> Settings --> Fiscal Localization`.
:guilabel:`Fiscal Localization` is located under the :guilabel:`Taxes` section.

.. seealso::
   - :doc:`../../fiscal_localizations`

For AvaTax this setting needs to be set to either :guilabel:`United States` or :guilabel:`Canada`.

Company settings
----------------

All companies operating under the Odoo database should have a full and complete address listed in
the settings. Navigate to :menuselection:`Settings App --> Companies`. Should there only be one
company operating the Odoo database, click :guilabel:`Update Info` to update the reliant contact
information for the company.

Should there be multiple companies operating in the database, click :guilabel:`Manage Companies` to
load a list of companies to select from. Update customer information by clicking into the specific
customer.

Database administrators should ensure that the :guilabel:`Street...`, :guilabel:`Street2...`,
:guilabel:`City`, :guilabel:`State`, :guilabel:`ZIP`, and :guilabel:`Country` are all updated for
the companies.

Module installation
-------------------

Next, ensure that the Odoo *AvaTax* module is installed. To do so, navigate to :menuselection:`Apps
application --> Search...` bar and then type in `avatax`. Press enter and the following results will
populate:

- :guilabel:`Avatax`: `account_avatax`
- :guilabel:`Avatax for SO`: `account_avatax_sale`
- :guilabel:`Avatax for Subscriptions`: `account_avatax_sale_subscription`
- :guilabel:`Avatax Brazil`: `l10n_br_avatax`
- :guilabel:`Avatax for SOs in Brazil`: `l10n_br_avatax_sale`
- :guilabel:`Account Avatax - Ecommerce`: `website_sale_account_avatax`
- :guilabel:`Account AvaTax - Ecommerce - Delivery`: `website_sale_delivery_avatax`

Click on the :guilabel:`Install` button on the module labeled :guilabel:`Avatax`: `account_avatax`.
This will install the following modules:

- :guilabel:`Avatax`: `account_avatax`
- :guilabel:`Avatax for SO`: `account_avatax_sale`
- :guilabel:`Account Avatax - Ecommerce`: `website_sale_account_avatax`

Should *AvaTax* be needed for Odoo *Subscriptions* or for delivery tax in Odoo *Ecommerce*, then
install those modules individually by clicking on :guilabel:`Install`. Additionally, in Brazil two
separate *AvaTax* modules need to be installed. See the list above for these modules.

.. _avatax/credentials:

Odoo AvaTax settings
====================

To integrate the *AvaTax* :abbr:`API (application programming interface)` with Odoo, go to
:menuselection:`Accounting --> Configuration --> Settings --> Taxes --> AvaTax` section. This is
where the *AvaTax* some configurations will be made and the credentials will be entered in.

.. image:: avatax/avatax-configuration-settings.png
   :align: center
   :alt: Configure Avatax settings

Prerequisites
-------------

Before the credentials are entered in, tick the checkbox to the right of the :guilabel:`AvaTax`
title to activate the feature.

Next, select the :guilabel:`Environment` that the company wishes to use AvaTax in. It can either be
:guilabel:`Sandbox` or :guilabel:`Production`.

.. seealso::
   For help determining which *AvaTax* environment to use (either :guilabel:`Production` or
   :guilabel:`Sandbox`), visit: `Sandbox vs Production environments
   <https://knowledge.avalara.com/bundle/fzc1692293626742/page/sandbox-vs-production.html>`_.

Credentials
-----------

Now, the credentials can be entered in. The AvaTax :guilabel:`Account ID` will be entered in the
:guilabel:`API ID` field and the :guilabel:`License Key` will be entered in the :guilabel:`API Key`
field.

.. tip::
   The :guilabel:`Account ID` can be found by logging into the AvaTax portal (`sandbox
   <https://sandbox.admin.avalara.com/>`_ or `production <https://admin.avalara.com/>`_). In the
   upper-right corner are the initials of the user and :guilabel:`Account`, click into this icon.
   The :guilabel:`Account ID` is listed first.

   To access the :guilabel:`License Key` see this documentation:
   :ref:`avatax/create_avalara_credentials`.

Transaction options
-------------------

There are two transactional settings that can be configured: :guilabel:`Use UPC Commit` and
:guilabel:`Commit Transactions`.

If the checkbox next to :guilabel:`Use UPC codes` is ticked then, the transactions will use
Universal Product Codes (UPC), instead of custom defined codes in Avalara. Consult a certified
public accountant (CPA) for specific guidance.

Should the :guilabel:`Commit Transactions` checkbox be ticked, then, the transactions in the Odoo
database will be committed for reporting in AvaTax.

Address validation
------------------

.. important::
   The :guilabel:`Address validation` feature only works with partners in North America.

Additionally, tick the checkbox next to the :guilabel:`Address validation` field.

.. important::
   For accurate tax calculations it is best practice to enter a complete address for the contacts
   saved in the database. However, AvaTax can still function by implementing a best effort attempt
   using only the :guilabel:`Country`, :guilabel:`State`, and :guilabel:`Zip code`. These are the
   three minimum required fields.

:guilabel:`Save` the settings to implement the configuration.

.. tip::
   Manually :guilabel:`Validate` the address by navigating to :menuselection:`Contacts app` and
   selecting a contact. Now that the AvaTax module have been configured on the database, a
   :guilabel:`Validate` button appears directly below the :guilabel:`Address`.

   Click :guilabel:`Validate` and a pop-up window appears with a :guilabel:`Validated Address` and
   :guilabel:`Original Address` listed. If the :guilabel:`Validated Address` is the correct mailing
   address for tax purposes click :guilabel:`Save Validated`.

   .. image:: avatax/validate-address.png
      :align: center
      :alt: Validate address pop-up window in Odoo with save validated button and validated address
            highlighted.

.. warning::
   All previously entered addresses for contacts in the Odoo database will need to be validated
   using the manually validate process outlined above. Addresses are not automatically validated if
   they were entered previously. This only occurs upon tax calculation.

Sync parameters
---------------

Upon finishing the configuration and settings of the AvaTax section click the :guilabel:`Sync
Parameters`. This action will synchronize the exemption codes from AvaTax.

.. _avatax/fiscal_positions:

Fiscal position
===============

Next, navigate to :menuselection:`Configuration --> Accounting --> Fiscal Positions`. A new
:guilabel:`Fiscal Position` is listed called :guilabel:`Automatic Tax Mapping (AvaTax)`. Click on
this :guilabel:`Fiscal Position`.

Ensure that the :guilabel:`Use AvaTax API` checkbox is ticked.

Optionally, tick the checkbox next to the field labeled: :guilabel:`Detect Automatically`. Should
this option be ticked, then, Odoo will automatically apply this :guilabel:`Fiscal Position` for
transactions in Odoo.

Specific parameters, such as :guilabel:`VAT required`, :guilabel:`Foreign Tax ID`,
:guilabel:`Country Group`, :guilabel:`Country`, :guilabel:`Federal States`, or :guilabel:`Zip Range`
can be specified below this checkbox.

.. warning::
   Should the :guilabel:`Detect Automatically` checkbox not be ticked, then each *Customer* will
   need to have the :guilabel:`Fiscal Position` set on their :guilabel:`Sales and Purchase` tab of
   the contact record. To do so, navigate to :menuselection:`Sales app --> Order --> Customers` or
   :menuselection:`Contacts app --> Contacts`. Then select and customer or contact to set the fiscal
   position on.

   Navigate to the :guilabel:`Sales and Purchase` tab and down to the section labeled
   :guilabel:`Fiscal Position`. Set the :guilabel:`Fiscal Position` field to the fiscal position
   for the customer.

   .. seealso::
      - :doc:`fiscal_positions`

AvaTax accounts
---------------

Upon selecting the checkbox option for :guilabel:`Use AvaTax API` a new :guilabel:`AvaTax` tab
appears. Click into this tab to reveal two different settings.

The first setting is the :guilabel:`AvaTax Invoice Account`, while the second is, :guilabel:`AvaTax
Refund Account`. Ensure both accounts are set for smooth end-of-year record keeping. Consult a
certified public accountant (CPA) for specific guidance on setting both accounts.

Click :guilabel:`Save` to implement the changes.

Tax mapping
===========

The AvaTax integration is available on Sale Orders and Invoices with the included AvaTax fiscal
position.

Product category mapping
------------------------

Before using the integration, specify an :guilabel:`Avatax Category` on the product categories.
Navigate to :menuselection:`Inventory --> Configuration --> Product Categories`. Select the product
category to add the :guilabel:`AvaTax Category` to. Finally next to the field labeled
:guilabel:`AvaTax Category`, click the drop-down menu and select a category, or :guilabel:`Search
More...` to find one that isn't connected.

.. image:: avatax/avatax-category.png
   :align: center
   :alt: Specify AvaTax Category on products

Product mapping
---------------

AvaTax Categories may be overridden or set on individual products as well. To set the
:guilabel:`Avatax Category` navigate to :menuselection:`Inventory app --> Products --> Products`.
Select the product to add the :guilabel:`Avatax Category` to. Under the :guilabel:`General
Information` tab, on the far-right, is a selector field labeled: :guilabel:`Avatax Category`.
Finally, click the drop-down menu and select a category, or :guilabel:`Search More...` to find one
that is not listed.

.. image:: avatax/override-avatax-product-category.png
   :align: center
   :alt: Override product categories as needed

.. important::
   Mapping an :guilabel:`AvaTax Category` on either the *Product* or *Product Category* should be
   completed for every *Product* or *Product Category*, depending the route that is chosen.
