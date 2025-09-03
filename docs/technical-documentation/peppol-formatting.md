# From Normal Invoice to PEPPOL UBL

To understand how a normal invoice is converted into a PEPPOL-compliant UBL invoice, it helps to think of the process like **addressing and sending a letter**.  
Each layer has its own purpose:

---

## 1. Business Model (EN 16931)

_Defines **what** data must be present in an invoice._
  
Examples:

  - Invoice ID  
  - Issue Date  
  - Seller and Buyer details  
  - At least one line with description, quantity, price, and tax  
  - Totals and payment information

These are called **Business Terms (BT-1 … BT-147)**.  

**Analogy:** the *content of the letter*.

---

## 2. Syntax Binding (UBL 2.1)

_Defines **how** to write the business model in a machine-readable format._

UBL = **Universal Business Language**, an XML schema maintained by OASIS.  

Example:  
  - BT-1 “Invoice number” →
    ```xml
    <cbc:ID>INV-2025-0001</cbc:ID>
    ```  
  - Placed inside the `<Invoice>` XML root element.  

**Analogy:** the *language the letter is written in*.

---

## 3. PEPPOL BIS Billing 3.0

_BIS = **Business Interoperability Specification**._

_PEPPOL specifies **exactly which options and codes** must be used._

Examples:

  - Must include `<cbc:ProfileID>` with a specific value.  
  - Currency codes must follow ISO 4217 (e.g. `EUR`).  
  - Units must follow UN/ECE codes (`EA` for “each”, `HUR` for “hour”).  
  - Parties must be identified with standardized schemes (`0208` = VAT number, `0088` = GLN, etc.).  

**Analogy:** the *strict format the post office requires for the envelope*.

---

## 4. Validation Artefacts (Schematron Rules)

_After creating a UBL file, it must be tested against EN 16931 and PEPPOL rules._

_Validation is performed with **Schematron**, an XML rule language._

Example rule:  

  - “Invoice must have at least one `<cac:AccountingSupplierParty>`.”  
  - If rules are not followed, the invoice is **rejected**.  

**Analogy:** the *postal worker checking if your address is correct before delivering*.

---

## 5. Transport (AS4 via PEPPOL Access Point)

- Invoices are **not sent by email**.  
- Instead, they are delivered through a **PEPPOL Access Point** (like an ISP for invoices).  
- The UBL invoice is wrapped in a **Standard Business Document Header (SBDH)** and transmitted securely using the **AS4 protocol**.


**Analogy:** the *postal service that delivers the letter to the recipient’s mailbox*.  

!!! AS4
    **AS4** stands for **Applicability Statement 4**.  
    It is a **communication protocol**: a set of technical rules about *how two computers exchange business documents over the internet*.
    
    ---
    
    Key points:
    
    - **AS2** was the older standard (often used in retail supply chains).  
    - **AS4** is the newer standard, built on **web services (SOAP)** with added **security and reliability**.
    
    ---
    
    Role in PEPPOL:
    
    - Your **UBL invoice** is wrapped into a secure **AS4 message** by your **Access Point**.  
    - The AS4 message is sent to the recipient’s Access Point, which unwraps it and delivers the invoice.  

---
