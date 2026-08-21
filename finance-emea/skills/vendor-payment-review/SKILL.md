---
name: vendor-payment-review
description: Review a vendor payment request against known fraud and error risk categories, including VAT and IBAN/SEPA validation, before it's approved for release. Use before releasing any vendor payment to an EMEA vendor.
user-invocable: false
---

# Vendor Payment Review (EMEA)

**Important**: This skill supports the accounts payable review process for EMEA entities. It does not replace Treasury sign-off or the VAT compliance checks owned by regional Tax.

Use this skill before any vendor payment is released to a vendor invoiced from an EMEA entity, to catch common fraud, error, and VAT/IBAN compliance issues.

## Step 1: Gather the payment request details

Collect the following before starting the review:

- Vendor legal name, country of registration, and VAT number
- Invoice number(s), invoice date, and due date
- Requested payment amount and currency (EUR, GBP, or local currency)
- IBAN and BIC/SWIFT on file vs. IBAN and BIC provided on the request
- Whether the payment is intra-EU, cross-border to a non-EU/EEA vendor, or domestic
- Supporting documentation (PO, contract, signed approval)

## Step 2: Check against known-risk categories

| Risk category | Description |
|---|---|
| VAT number invalid or unregistered | Vendor's VAT number does not validate against VIES (VAT Information Exchange System) |
| IBAN/BIC mismatch | IBAN provided does not correspond to the vendor's registered country or the BIC on file |
| Cross-border payment to non-EU vendor | Payment leaves the EU/EEA, triggering additional withholding or reporting requirements |
| Requested change to SEPA mandate | Vendor has asked to switch from SEPA direct debit to a manual bank transfer |
| Invoice missing VAT breakdown | Invoice does not show VAT separately, or cites the wrong VAT rate for the vendor's country |

### 🔴 Red flag: IBAN/BIC mismatch

- Cross-check the IBAN's country code against the vendor's registered country and the BIC on file
- If the IBAN was recently changed, treat it with the same caution as any other payment redirection attempt and confirm with the vendor before using it
- Do not release payment on a mismatched IBAN without direct vendor confirmation through a known contact channel

### 🔴 Red flag: VAT number invalid or unregistered

- Re-validate through VIES before assuming a data-entry error
- If the vendor genuinely has no valid VAT number, confirm with regional Tax whether the reverse-charge mechanism applies instead of withholding payment outright

## Step 3: Flag findings

For any risk category matched in Step 2:

1. Document which risk categories were matched and why, including the VIES/IBAN validation result
2. Route the payment request to the EMEA AP Lead for secondary review before release
3. Do not release the payment until all flagged items are cleared and documented
4. Loop in regional Tax for any VAT-related flag before releasing payment

## Output

Provide a short summary: vendor name, entity, amount, currency, risk categories matched (if any), and the recommended next step (release, hold for review, or escalate).
