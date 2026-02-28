# Power Platform – Reusable Document + Approval Automation (PoC)

This repo packages a reusable **Power Automate “Document Service”** pattern:
- Power Apps passes structured data + parameters
- Flow generates **HTML → PDF/Excel**
- Stores output (SharePoint/OneDrive)
- Optional **Approvals**
- Optional **Master Data writeback**
- Full **logging/monitoring** hooks for production

---

## What’s in here

- `docs/architecture.md`  
  Modular blueprint (child-flow pattern), governance, monitoring.

- `docs/use-cases.md`  
  Concise PoC → Workflow → Use cases → Features summaries.

- `flow_export/`  
  Place your exported Power Automate package here (see steps below).

- `powerapps_samples/`  
  Example payload schemas + Power Apps calling pattern.

---

## Quick Start (Power Automate)

### 1) Export the flow (attach it to this repo)
In Power Automate:
1. Open your flow
2. **Export → Package (.zip)**
3. Choose **"Update"** for connectors if needed when importing elsewhere
4. Download the zip
5. Put it into: `flow_export/YourFlowName.package.zip`

> If you also use child flows, export each one and store them in `flow_export/child_flows/`.

### 2) Import in another environment
1. **My flows → Import**
2. Upload the package zip from `flow_export/`
3. Fix connections (SharePoint/OneDrive/Outlook/Approvals)
4. Save → Test from Power Apps

---

## Power Apps → Flow interface (recommended)
Pass a single JSON payload with:
- `documentType`
- `templateName`
- `outputFormat` (PDF/Excel/Both)
- `approverEmail`
- `saveLocation`
- `data` (your form fields)

See `powerapps_samples/payload.example.json`.

---

## Production notes
- Prefer **child flows** for: validation, document generation, approvals, logging, writeback
- Add **Scopes** for Try/Catch and log failures
- Add correlation IDs + run metadata for traceability

---

## License
MIT
