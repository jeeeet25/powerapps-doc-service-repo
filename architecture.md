# Architecture (Production Pattern)

## Core idea
Treat the flow as a **Document Service** that Power Apps (or other flows) can call with parameters.

## Recommended modules (child flows)
1. **Validation Flow**
   - schema checks, required fields, type checks
2. **Document Generation Flow**
   - compose HTML from template + data
   - create file (SharePoint/OneDrive)
   - convert to PDF (OneDrive connector)
3. **Approval Flow (optional)**
   - Start and wait for approval
   - capture approver comments + decision
4. **Writeback Flow (optional)**
   - update Dataverse/SQL/SharePoint master data
5. **Logging/Observability Flow**
   - success/failure logs
   - correlation ID
   - run metrics (duration, output link, status)

## Governance
- Naming convention: `DOCSVC.<module>.<purpose>`
- Store templates in SharePoint Library (versioned)
- Capture: requestor, timestamp, environment, correlation ID

## Monitoring
- On failure: log error details + notify support channel/email
- Power BI dashboard over the log table/list:
  - volume, success rate, top failures, processing time, SLA breaches
