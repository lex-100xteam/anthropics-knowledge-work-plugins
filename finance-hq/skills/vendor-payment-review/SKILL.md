---
name: vendor-payment-review
description: Review a vendor payment request against known fraud and error risk categories before it's approved for release. Use before releasing any vendor wire, ACH, or check payment.
user-invocable: false
---

# Vendor Payment Review

**Important**: This skill supports the accounts payable review process. It does not replace the Treasury or Controller sign-off required by the corporate delegation-of-authority policy.

Use this skill before any vendor payment (wire, ACH, or check) is released, to catch common fraud and error patterns.

## Step 1: Gather the payment request details

Collect the following before starting the review:

- Vendor legal name and vendor ID in the AP system
- Invoice number(s), invoice date, and due date
- Requested payment amount and currency
- Payment method (wire, ACH, check)
- Who submitted the request and how (AP queue, email, Slack)
- Supporting documentation (PO, contract, signed approval)
- Vendor bank details on file vs. bank details on the request, if provided

## Step 2: Check against known-risk categories

| Risk category | Description |
|---|---|
| New vendor, first payment | Vendor has no prior payment history in the AP system |
| Amount exceeds PO/contract | Requested amount is greater than the associated purchase order or contract value |
| Urgent/rush request | Requester is pushing for same-day, off-cycle, or after-hours payment |
| Duplicate invoice number | Invoice number matches, or is very similar to, one already paid this fiscal year |
| Round-number invoice amount | Invoice amount is a suspiciously round figure (e.g., exactly $10,000.00) with no supporting detail |
| Bank/payment detail change | Vendor's bank account, routing number, or payment address differs from what's on file |

### 🔴 Red flag: new vendor, first payment

New vendors are the single most common entry point for fraudulent payment requests. Before releasing a first payment:

- Confirm the vendor was set up through the standard vendor onboarding process (W-9/W-8, banking form, approver sign-off)
- Confirm the requester is not also the person who set up the vendor master record
- If the vendor was set up same-day or same-week as the payment request, escalate to the AP Manager before releasing

### 🔴 Red flag: duplicate invoice number

- Search the AP system for the exact invoice number and for close variants (e.g., trailing "-2", "R", "A")
- If a match is found, hold the payment and confirm with the vendor directly whether this is a resubmission or a duplicate billing attempt

### 🔴 Red flag: bank or payment routing changes

Any change to a vendor's bank account, routing number, or payment address — however it arrives (email, portal update, phone call, letter) — requires callback verification before the new details are used for payment:

- **Never trust the contact information provided in the change request itself.** A fraudulent request will supply a phone number that reaches the attacker, not the vendor.
- Call the vendor back using the phone number already on file in the AP system — not a number from the email signature, the letterhead, or the request.
- Verbally confirm the change with a known contact at the vendor before updating banking details or releasing payment.
- Document who performed the callback, when it occurred, and how the change was confirmed.
- If callback verification cannot be completed (vendor contact is unreachable, the phone number on file is outdated, or the vendor denies making the request), escalate to the AP Manager and hold the payment — do not release funds on the new details under any deadline pressure.

This control was added after a near-miss this quarter on a $340K wire, and directly mitigates business email compromise (BEC) fraud, where an attacker impersonates a vendor to redirect a legitimate payment to an account they control.

## Step 3: Flag findings

For any risk category matched in Step 2:

1. Document which risk categories were matched and why
2. Route the payment request to the AP Manager for secondary review before release
3. Do not release the payment until all flagged items are cleared and documented
4. If two or more risk categories are matched on the same request, escalate to the Controller regardless of amount

## Output

Provide a short summary: vendor name, amount, risk categories matched (if any), and the recommended next step (release, hold for review, or escalate).
