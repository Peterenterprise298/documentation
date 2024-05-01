===============
Tax calculation
===============

Automatically calculate taxes on Odoo quotations and invoices with Avatax by confirming the
documents. Alternatively, calculate the taxes manually by clicking the :guilabel:`Compute taxes
using Avatax` button while these documents are in draft mode.

.. tip::
   Clicking the :guilabel:`Compute taxes using Avatax` will recalculate taxes should any product
   lines be edited on the invoice.

.. image:: calculate-avatax.png
   :align: center
   :alt: Sales quotation with the confirm and compute taxes using AvaTax buttons highlighted.

The tax calculation is automatically triggered during the following circumstances:

**Auto Triggers**
- Sales rep sends the quote by email with :guilabel:`Send by email` button (pop-up).
- When the customer views the online quote on the portal.
- When a quote is confirmed into as sales order.
- When the customer views the invoice on the portal.
- When a draft invoice is validated.
- When the customer views the subscription in the portal.
- When a subscription generates an invoice.
- When the customer gets to the last screen of the ecommerce checkout.

**Manual Triggers**
- :guilabel:`Compute taxes using Avatax` button at the bottom of the quote.
- :guilabel:`Compute taxes using Avatax` button at the top of the invoice.

.. tip::
   Use the :guilabel:`Avalara Code` field that is available on customers, quotations, and invoices
   to cross-reference data in Odoo and Avatax. This field is located under the :menuselection:`Other
   info` tab of the sales order or quotation in the :guilabel:`Sales` section.

.. important::
   On other documents, such as invoices and subscriptions, there are also automatic and manual
   triggers for the AvaTax calculation. The :guilabel:`Automatic Tax Mapping (AvaTax)` fiscal
   position is also applied on those Odoo documents.

.. seealso::
   - :doc:`../fiscal_positions`

======================
AvaTax synchronization
======================

Synchronization occurs with AvaTax, when the *invoice* is created in Odoo. This means the sales tax
is recorded with Avalara.

To do so, navigate to :menuselection:`Sales app --> Orders --> Quotations`. Select a quotation from
the list.

After confirming a quotation and validating the delivery, click :guilabel:`Create Invoice`. Indicate
whether it is a :guilabel:`Regular invoice`, :guilabel:`Down payment (percentage)`, or
:guilabel:`Down payment` (fixed amount).

Then click :guilabel:`Create and view invoice`. The recorded taxes can be seen in the
:guilabel:`Journal Items` tab of the invoice. There will be different taxes depending on the
location of the :guilabel:`Delivery Address`.

Finally, press the :guilabel:`Confirm` button to complete the invoice and synchronize with the
AvaTax portal.

.. warning::
   An invoice cannot be :guilabel:`Reset to draft` because this causes de-synchronization with the
   AvaTax Portal. Instead, click and :guilabel:`Add credit note` and state: `Sync with AvaTax
   Portal`.
