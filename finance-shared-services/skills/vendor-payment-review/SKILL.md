---
name: vendor-payment-review
description: Review a vendor payment request against known fraud and error risk categories under the maker-checker dual-control model, before it's approved for release. Use before releasing any vendor payment processed on behalf of a client business unit.
user-invocable: false
---

# Vendor Payment Review (Shared Services)

**Important**: This skill supports the outsourced accounts payable review process. This team processes payments on behalf of client business units under a maker-checker model — every step below assumes segregation of duties between the preparer (maker) and the approver (checker).

Use this skill before any vendor payment batch is released, to catch common fraud, error, and control-bypass patterns.

## Step 1: Gather the payment request details

Collect the following before starting the review:

- Client business unit code and vendor ID in the client's AP system
- Invoice number(s), invoice date, and due date
- Requested payment amount and currency
- Name of the maker who prepared the batch and the checker assigned to approve it
- Supporting documentation and the approval trail from the client's ERP
- Whether any vendor master data was edited as part of preparing this batch, and by whom

## Step 2: Check against known-risk categories

| Risk category | Description |
|---|---|
| Missing checker sign-off | Payment batch has a maker but no independent checker approval recorded |
| Maker and checker are the same person | Segregation-of-duties control has been bypassed |
| Split invoice under approval threshold | A single order has been broken into multiple invoices, each just under the client's approval threshold |
| Vendor master data changed by the processing team | Vendor bank or contact details were edited by shared-services staff rather than the client's vendor management team |
| Batch contains a new client business unit | Payment batch references a client entity not previously seen in this queue |

### 🔴 Red flag: maker and checker are the same person

- This should be structurally impossible in the AP system; if it happens, treat it as a system control failure, not just a process exception
- Hold the batch and notify the Shared Services Controls lead immediately

### 🔴 Red flag: vendor master data changed by the processing team

- Shared-services staff should never be able to edit vendor bank details directly — that is reserved for the client's vendor management team
- If a change appears in the audit trail as made by a processor, treat it as a potential control breach and escalate before touching any payment against that vendor

## Step 3: Flag findings

For any risk category matched in Step 2:

1. Document which risk categories were matched and why, including maker and checker names
2. Route the batch to the Shared Services Controls lead for secondary review before release
3. Do not release any payment in the batch until all flagged items are cleared and documented
4. Any segregation-of-duties bypass (maker = checker, or missing checker) must be reported to the client's Controller, not just resolved internally

## Output

Provide a short summary: client business unit, vendor name, amount, risk categories matched (if any), and the recommended next step (release, hold for review, or escalate).
