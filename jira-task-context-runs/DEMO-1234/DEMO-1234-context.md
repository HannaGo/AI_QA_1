# DEMO-1234 — Apply discount code at checkout

Source: `https://demo-jira.example.com/browse/DEMO-1234`
Type: Story
Generated: 2026-09-29

## Goal

Add a discount code input on the checkout summary step so customers can reduce the order total before payment.

## Boundaries

- In scope: the "Discount code" input field and "Apply" button on the checkout summary step, code validation, displaying the reduced total, showing an inline error for invalid or expired codes, applying one code per order.
- Out of scope: payment processing, shipping/address collection, other promotions, and the order completion button itself.

## Requirements

- Display a "Discount code" input field on the checkout summary step.
- Allow the customer to type or paste a code up to 20 characters.
- Clicking "Apply" validates the code against the backend.
- If the code is valid, reduce the order total and display the new total.
- If the code is invalid or expired, show the inline error "Invalid or expired discount code" below the input.
- Only one discount code can be applied per order.
- Tax is calculated based on the discounted total.

## Additional requirements (from comments)

- Discount code matching is case-insensitive; `PROMO10` and `promo10` are treated as the same code (comment by dev-oleh, 2026-09-25).

## Related Jira context

> This section is for context reference only. It is not a requirement of the current task and is not subject to processing by the next skills.

- DEMO-1000: Epic "Checkout improvements" — the discount code feature is part of the broader checkout flow.

## Attachments

- `checkout-mockup-v2.png` (PNG) — shows the placement of the "Discount code" input and "Apply" button. Not processed because the attachment was not downloaded.
- `terms.pdf` (PDF) — discount terms and conditions. Not processed because the attachment was not downloaded.
