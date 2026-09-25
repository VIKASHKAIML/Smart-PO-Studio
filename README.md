# SmartPO Studio — Purchase Order Data Extractor

A lightweight, modern web-based workbench designed to extract, review, edit, and export structured data from Purchase Orders (POs), supplier invoices, and quotations.

SmartPO Studio operates with a dual-engine architecture:
1. **AI Vision & NLP (Google Gemini):** Zero-shot multimodal schema extraction directly from raw text or uploaded documents.
2. **Local Intelligent Heuristics & OCR:** Zero-fail deterministic extraction engine that operates completely in-browser without sending data over external APIs.

---

## 🚀 Key Features

- **Side-by-Side Verification Workbench:** Compare raw input documents or images on the left against the editable parsed purchase order form on the right.
- **Dual Extraction Engines:**
  - **Auto (Gemini AI with Fallback):** Sends unstructured text or image inputs to Gemini for schema-guided extraction.
  - **Local Heuristics Only:** Uses high-precision regular expressions, token analyzers, and numeric normalizers directly in the browser.
- **OCR Support (Tesseract.js):** Extract text automatically from uploaded PO images, receipts, and scans when running locally.
- **Dynamic Line Items Grid:**
  - Real-time row-by-row mathematical recalculations ($Qty \times Price \times [1 + Tax\%]$).
  - Add, edit, or delete items on the fly.
  - Automatic reconciliation of subtotal, tax amounts, freight/shipping, and discounts.
- **Multi-Format Export & Archival:**
  - Export structured orders as **JSON** or tabular **CSV**.
  - Print-ready format (`Ctrl/Cmd + P` or dedicated **Print** action).
  - Session history drawer allowing you to approve, save, and restore purchase orders at any time.

---

## 🛠️ Project Structure

This project follows a portable, single-file architecture:

```text
├── index.html        # Complete single-page application (UI, styles, scripts, parsers)
└── README.md         # Documentation and setup guide
```

---

## 💻 Getting Started

### 1. Run Directly in the Browser
No Node.js or backend servers are required. Simply open `index.html` in any modern web browser:

```bash
# On macOS
open index.html

# On Linux
xdg-open index.html

# On Windows
start index.html
```

Or serve with any static web server:
```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```

### 2. Configure Gemini API Key (Optional)
By default, the application runs using the local heuristic parsing engine. To activate Gemini AI multimodal parsing:
1. Click the **API Config** button in the top navigation bar.
2. Enter your Google Gemini API key.
3. Click **Test Key** to verify connectivity, then click **Save Configuration**.
4. The key is securely saved to your browser's `localStorage`.

---

## 📋 Extraction Schema Reference

The extractor structures purchase order documents into the following JSON schema:

```json
{
  "poNumber": "PO-2026-9021",
  "issueDate": "2026-09-24",
  "dueDate": "2026-10-15",
  "paymentTerms": "Net 30 days",
  "currency": "$",
  "vendor": {
    "name": "Quantum Cloud Components Inc.",
    "address": "1200 Silicon Avenue, Austin, TX 78701",
    "contact": "sales@quantumcloud.com",
    "taxId": "TX-449102-A"
  },
  "buyer": {
    "name": "Acrobyte Systems Corp",
    "address": "500 Tech Parkway, San Jose, CA 95110",
    "contact": "procurement@acrobyte.io",
    "taxId": "US-88291039"
  },
  "items": [
    {
      "description": "Enterprise Rack Server R750",
      "sku": "SRV-750-X",
      "quantity": 2,
      "unitPrice": 3200.00,
      "taxRate": 8.25
    }
  ],
  "shipping": 120.00,
  "discount": 150.00,
  "notes": "Verified against procurement contract terms."
}
```

---

## 📦 Dependencies

All third-party libraries are loaded via CDN:
- [Tailwind CSS](https://tailwindcss.com/) — Utility-first styling
- [Lucide Icons](https://lucide.dev/) — UI iconography
- [Tesseract.js](https://tesseract.projectnaptha.com/) — Client-side optical character recognition (OCR)
- [Inter & JetBrains Mono](https://fonts.google.com/) — Typography

---

## 📄 License
This project is open-source and free to adapt for procurement operations, ERP pipelines, and internal tools.