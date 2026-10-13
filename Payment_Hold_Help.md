# Payment Hold Help

**In 30 seconds:** Suresh sees ₹14,999 on hold on one payment, understands why, adds his bill (checked on the phone), reviews an editable letter in Hindi and English, confirms with an OTP, and tracks the grievance on a dated timeline. Everything below is supporting detail.

A proposed feature inside the Razorpay Payments for Business mobile app. When police hold a payment, the merchant understands the hold and gets a complete grievance to Razorpay quickly. Target: prepare and submit to Razorpay in under two minutes, with evidence ready.

> About ₹8.26 lakh was frozen from August 2025 until a June 2026 High Court order directed defreezing over a ₹1,000 sale. (Sri Sai Wines v. Union of India, W.P. 969/2026, Andhra Pradesh High Court, order of 22 June 2026. The order names no payment aggregator. It shows how severe a hold can be, not how often Razorpay merchants face one, and it does not tell us when the bank actually released the funds.)

*Independent concept prototype. Sample data. No submission is sent. Not a Razorpay product, not legal advice.*

## Annotation key

- **Observed Razorpay UI**: the five-tab shell, greeting, account overview, settlement preview, analytics and collection tools, as described in the brief's reference screenshots. Not pixel-verified here.
- **Proposed addition**: everything Payment Hold Help adds.
- **Assumption requiring confirmation**: operational points below.

## Where it lives in the app

Five tabs unchanged: Home, Payments, Products, Support, Account. Payment Hold Help is contextual, not a sixth tab.

- **Home** (proposed): attention card "₹14,999 on hold, police-linked restriction on one payment, Get help with this hold". After submission: "Grievance pack submitted, View your next step, Track your grievance".
- **Payments → Settlements** (proposed): "On hold" summary and status filter. Held funds sit apart from the ₹2,84,560 scheduled settlement, which is a schedule, not a bank balance or guaranteed arrival.
- **Payment detail** (proposed): separate statuses for payment (captured), hold (police-linked), grievance and settlement (on hold). A captured payment is never shown as failed. Actions: View hold details, Get help with this hold, then Track your grievance.
- **Support** (proposed): Payment Hold Help, Existing grievances, Bank account restricted?

The settlements doc describes navigation as Transactions then Settlements, with Date and Status filters. The brief's baseline uses a Payments tab. Confirm against the current build; do not mix app versions.

## Merchant and scenario

Suresh K., a fictional phone-shop owner in Lucknow who prefers Hindi. ₹14,999 paid by Razorpay QR / UPI on 6 Oct 2026, 7:42 PM. Payment ID pay_Q7XK2m9LfT1aB3, UTR 523419887361, invoice LMP/2026/1187, ledger updated 13 Oct 2026, 4:14 PM. Payment ID, UTR, police complaint reference, Razorpay intake receipt (FS-2026-0142) and institutional acknowledgment are all different records and are never conflated.

## Workflow (English and Hindi)

1. **Payment on hold.** Amount, linked payment, authority, state, complaint reference. "This payment is linked to a reported fraud investigation. The hold is not a finding that you committed fraud." Options: This was a real sale; I don't recognise this payment (flag to compliance, no refund); Something else? Talk to support. Collapsed original notice; in Hindi the translation is assistance and the original prevails.
2. **Add supporting documents.** Added from payment records: transaction record and hold reference (both appear in the screen, the letter's enclosure list and the pack). Documents you provide: bill or invoice (needed for this case), optional handover/CCTV, optional customer communication, optional IMEI. Photo check: "Photo quality check passed. Sharpness, lighting and size checked. Please confirm the details are legible." IMEI: "IMEI digit check passed. This does not verify the device or prove delivery." Replace, remove, retry, save draft.
3. **Optional AI.** "Read bill" and "Help write my explanation", each behind a disclosure that the photo or text goes to an AI service. Manual route always available. Editable fields, mismatch flags, not-read fields shown blank. AI must not add facts. Sample output is labelled when live AI is unavailable.
4. **Submit grievance.** Editable explanation and letter, exact attachment list, accuracy confirmation, "Confirm and submit", OTP. In Hindi mode a Hindi summary of the facts, request and enclosures sits above the English letter, with an optional AI Hindi translation of the final explanation (marked outdated if the explanation changes) and the merchant's original words beside any AI-written text. The summary cannot reflect free edits to the letter and says so. Any change to the explanation, letter or attachments clears the accuracy confirmation, and an edited letter that no longer matches its attachments blocks submission until the merchant updates the enclosure list, resets the letter, or confirms it was checked.
5. **Grievance pack received.** Razorpay intake receipt and timestamp, View grievance letter and Copy letter text (a real document-and-attachment export is not built, so the app does not claim a download), Track your grievance, Contact support. "Razorpay reviews your pack and coordinates the next step. The proposed institutional filing route is through Razorpay or its nodal bank, subject to confirmation." The OTP confirms submission; it is not a legal digital signature.
6. **Track your grievance.** Dated timeline of completed events, one next step, future dates in a separate dashed box. Institutional acknowledgment appears only once filing is confirmed.

## Tracker branches (each forward-only)

Stages: received by Razorpay, evidence review, institutional filing confirmed, with investigating officer, decision or escalation, release instructed, hold removed, settlement processed. Deadlines run from the applicable event, not the first alert.

- Between "hold removed" and "settlement processed" the payment shows "Hold removed · Awaiting settlement" everywhere.
- **Ordinary release.** 13 Oct received. 15 Oct filing and officer receipt confirmed (decision due 30 Oct). 22 Oct decision and release instructed (early is valid). 23 Oct hold removed and settlement processed.
- **No decision in 15 days.** 30 Oct window ends. 31 Oct escalated to the District Grievance Officer (district decision due 15 Nov). Simulated district decision 9 Nov. Release instructed 10 Nov. Hold removed and settled 11 Nov. It never returns to the 22/23 Oct sequence.
- **Officer keeps the hold.** 24 Oct decision and reasons received; review window to 8 Nov. "Request review" is the only way to reach "Review requested". Then district receipt 29 Oct (review due 13 Nov), simulated decision, and either release or closure with the hold continuing.
- **More evidence needed.** Only before filing. Document request, merchant response, original 13 Oct 4:16 PM receipt and 20 Oct filing target preserved, then review, filing and release.
- **Closed cases** hide every outcome-changing action and show a summary. Scenario switching exists only in the presenter panel.

The 7-day filing target (20 Oct) applies the SOP's institution timeline to Razorpay, which is an assumption. The 15-day, review and 2-day clocks follow the MHA SOP (2 Jan 2026), paragraphs 10 to 10.3.

## How merchants cope today (hypothesis, not observed)

Notice a settlement shortfall. Call support or the bank. Work out which payment is involved. Find the bill and chat. Write an explanation. Follow up with no clear clock. We have not interviewed merchants; validating this baseline is the first next step.

## Why mobile, and the three product decisions

The camera (bill, counter), customer chat, QR payment and Hindi assistance are already on the merchant's phone, and he is working between customers. Decisions: start from the hold rather than a blank form; reuse authoritative payment records; keep AI optional, with the merchant reviewing every field and the letter.

## How AI was used in the build

Claude and Claude Code built the prototype, the English and Hindi copy and the sample assets, verified claims against primary sources such as the official SOP, and ran scripted browser tests (Playwright) across the main flow, all five tracker outcomes, the failure states, Hindi, and a phone-width dark-mode view. ChatGPT/Codex audited the notes and source code over several rounds, and each finding was checked against sources or reproduced before any change. I also checked the prototype in the browser myself.

One concrete before and after: a review flagged the tracker; a test reproduced it (after escalation, the next update jumped back to the 22/23 Oct release dates); it was rebuilt as separate forward-only timelines per outcome, and re-tested for all five outcomes. Other corrections of this kind: the merchant-files-in-the-portal assumption (fixed against the official SOP), an overclaiming "valid IMEI" label, a retry bug on real uploads, and a hold shown as active after removal. No productivity multiple is claimed.

## Bank-account helper (Support)

"This prepares records for Razorpay payments. Other transactions or complaints may also affect your bank account." Provides the Razorpay payment record, an editable bank-branch letter and a branch-visit checklist, asking the bank to review the restriction and use its own grievance route. Razorpay cannot remove a bank freeze, and the app does not imply it can.

## States covered

Upload failure and retry; AI unavailable; missing evidence; submission failure (no success shown); institutional acknowledgment unavailable; external status unavailable; additional-evidence request; closed-case summary. Language switching and back-navigation keep drafts, attachments, identifiers and progress.

## What exists today

Bank grievance desks. Cashfree's public grievance policy (proof of good-faith provision on police alerts, tracking by email or dashboard). Account Freeze Navigator advertises a ₹499 offer; we have not verified purchases or outcomes. Lawyers. Our angle is the combination: integrated hold context, Razorpay payment records, evidence preparation and institutional coordination, inside the app the merchant already uses. We found no public equivalent inside a payment app; private features cannot be ruled out. We do not claim to be first.

## Measurement

North star: first-time completeness, the share of packs accepted as complete for institutional filing without further merchant documents. It holds whether Razorpay or its nodal bank files, and it is not approval. Also: submission to confirmed filing, active time to submit without autofill, completion and abandonment. External outcomes (15-day decisions, release time) are tracked against a baseline before attributing change. Guardrails: wrong AI extraction, mismatched payments, missed deadlines, duplicate filings, misleading status.

## Assumptions requiring confirmation

- Razorpay files in the grievance module itself or through its nodal bank. The SOP does not explicitly assign filing to Razorpay.
- What status Razorpay can see and share, and when it may notify merchants (including where notices restrict disclosure).
- Incidence of police-linked holds among Razorpay merchants.
- Two minutes is a target, unproven without autofill, with missing evidence or several complaints.
- OTP versus a recognised e-signature; AI vendor, data handling and retention.
- Notice text, reasons and dates are samples.

## Not built

Direct filing into police systems, refunds or unfreezing, a lawyer marketplace, chargebacks, generic KYC or risk tools.

## Prototype notes

The Razorpay logo is not embedded and must be loaded through the presenter panel each session; the prototype does not claim to reproduce Razorpay's app exactly. Colours and type approximate a Razorpay-like look and are not Blade tokens. Photo and IMEI checks run in the browser; bill reading and rewriting use an AI call only if the viewer allows it, otherwise labelled sample output. Timer lives in the presenter panel only.

## Sources

- [Razorpay Payments app on Google Play](https://play.google.com/store/apps/details?id=com.razorpay.payments.app), [mobile app docs](https://razorpay.com/docs/payments/mobile-app/), [settlements in the app](https://razorpay.com/docs/payments/mobile-app/track-manage/view-settlements/), [brand assets](https://razorpay.com/newsroom/brand-assets/), [Blade](https://blade.razorpay.com/), [RazorSense](https://razorpay.com/razorsense/)
- [MHA SOP for NCRP-CFCFRMS, 2 Jan 2026](https://meghalayahighcourt.nic.in/sites/default/files/news/N347.pdf)
- [Supreme Court proceedings, 9 Feb 2026](https://cdnbbsr.s3waas.gov.in/s3ec0277ee3bc58ce560b86c2b59363281/uploads/2026/04/2026042314.pdf)
- [PIB: CFCFRMS 2.0, 28 Jul 2026](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2290377&lang=1&reg=22)
- [Sri Sai Wines order](https://www.livelaw.in/pdf_upload/2026/07/06/1-2-684649.pdf) and [LiveLaw report](https://www.livelaw.in/high-court/andhra-pradesh-high-court/andhra-pradesh-high-court-vendors-verify-upi-customer-antecedents-540137)
- [Telangana Today](https://telanganatoday.com/shopkeepers-pay-the-price-for-fraudsters-qr-payments-in-telangana)
- [Razorpay: how gateways handle LEA hold requests, June 2026](https://razorpay.com/blog/how-payment-gateways-handle-law-enforcement-agency-lea-hold-requests-in-india/)
- [Cashfree grievance policy](https://www.cashfree.com/grievance-redressal-policy/), [Account Freeze Navigator](https://accountfreezenavigator.com/)

All merchant, payer, police and reference details are invented.
