# Auburn Orthodontics — Deposit Match PPC Landing Page

Static, dependency-free landing page for the **We Match Your Down Payment — Up to $1,000 Off Braces or Invisalign®** campaign.

```
index.html          Landing page (all CSS/JS inline for a single-request render)
thank-you.html      Conversion page shown after a successful form submission
assets/img/         Logo and Dr. Steinhart photo (WebP, two sizes)
assets/fonts/       Self-hosted Manrope variable font (latin subset, 25 KB)
```

## Before launch — fill in `CONFIG` at the bottom of `index.html`

| Key | What to set |
| --- | --- |
| `formEndpoint` | GHL / LeadConnector **inbound webhook** URL. The form POSTs JSON with `first_name`, `last_name`, `phone`, `email`, `planned_down_payment`, `consent`, `offer`, `source_page`, `page_url`, `submitted_at`. Leave empty and set the `<form action="">` instead if you prefer a standard POST. |
| `thankYouUrl` | Redirect after success (default `thank-you.html`, which pushes a `generate_lead` dataLayer event for the Google Ads conversion). |
| `gtmId` | GTM container ID. GA4, Google Ads conversion, Meta Pixel and call tracking should live in the container. Also set it in `thank-you.html`. |
| `turnstileSiteKey` / `recaptchaSiteKey` | Optional visible challenge. A honeypot field and a minimum-fill-time check always run; the approved error copy "Please complete the challenge and try again." is shown on failure. |

To use the existing LeadConnector **embedded form** instead of the native form, replace the `<form id="lead-form">…</form>` block with the GHL `<iframe>` embed. Keep the surrounding `.form-card` wrapper and the `id="offer-form"` so every CTA still scrolls to it.

### dataLayer events
`phone_click`, `cta_click`, `directions_click` (with `location`), `form_submit`, `form_submit_success` (with `planned_down_payment`), and `generate_lead` on the thank-you page.

## Images
- `assets/img/logo-white.webp` — supplied logo (white mark, used on navy).
- `assets/img/dr-todd-steinhart-480.webp` / `-800.webp` — supplied, verified photo of Dr. Todd Steinhart, served via `srcset`.
- Optional practice / patient imagery can be added to the final CTA section. No stock photography is used.

## Reviews ticker
Seven authentic Google reviews run in a CSS-only ticker (`.ticker` / `.track`). The list is duplicated once (second copy `aria-hidden`) for a seamless loop; it pauses on hover/focus and becomes a plain swipeable row under `prefers-reduced-motion`. To add a review, add the same `<li class="review">` to both copies.

## Content flags for client review
- **Early Crowding & Expansion** — the source duplicated the airway text. The card uses only the approved "Proactive Growth Guidance" wording.
- **FAQ answers** — the source listed questions only. Answers are assembled verbatim from approved page copy (offer mechanics, timing philosophy, Invisalign and smile-simulation copy).
- **"discrete" → "discreet"** spelling corrected in the Adult Smile Transformations copy.
- Patient reviews are preserved word-for-word, including references to "Woloshyn".
- `<meta name="robots" content="noindex">` is set, as is typical for paid landing pages. Remove it if the page should be indexed.
