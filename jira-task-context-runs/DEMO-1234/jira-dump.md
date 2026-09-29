# DEMO-1234 — Apply discount code at checkout

## Jira fields

- **Summary:** Apply discount code at checkout
- **Issue type:** Story
- **Epic link:** DEMO-1000
- **Description:**

As a customer, I want to enter a discount code on the checkout page so that I can get a reduced price before I complete the payment.

Acceptance criteria:

1. A "Discount code" input field is visible on the checkout summary step.
2. The customer can type or paste a code up to 20 characters.
3. Clicking "Apply" validates the code against the backend.
4. If the code is valid, the order total is reduced and the new total is shown.
5. If the code is invalid or expired, an inline error "Invalid or expired discount code" is shown below the input.
6. Only one discount code can be applied per order.

- **Acceptance criteria (customfield_10001):**
  - A "Discount code" input field is visible on the checkout summary step.
  - The customer can type or paste a code up to 20 characters.
  - Clicking "Apply" validates the code against the backend.
  - If the code is valid, the order total is reduced and the new total is shown.
  - If the code is invalid or expired, an inline error "Invalid or expired discount code" is shown below the input.
  - Only one discount code can be applied per order.

- **Notes for QA (customfield_10003):**
  - Check that the field accepts alphanumeric codes.
  - Verify the error message text exactly matches the acceptance criteria.

## Comments

- **2026-09-25, dev-oleh:** "Discount codes should be case-insensitive (PROMO10 and promo10 are the same)."
- **2026-09-26, pm-anna:** "Please confirm this doesn't affect tax calculation. Tax is based on the discounted total."
- **2026-09-27, qa-maria:** "I'll start testing once the build is ready."

## Attachments

- `checkout-mockup-v2.png` (PNG) — mockup of the discount code input and apply button placement.
- `terms.pdf` (PDF) — terms and conditions for discount usage.

## Related issues

- DEMO-1000: Epic "Checkout improvements" — discount code is part of the checkout flow.
