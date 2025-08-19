# SkillOnNet Test Email – Implementation & Documentation

**Author:** Migle Matiukaite  
**Template:** Single‑column promotional email with hero background image, CTA, responsive + dark‑mode support.  
**Width:** 600px (max) container.

---

## 1) Files included

- `index.html` – the email template [(email_template.html)].
- `README.md` – this document.

> Note: Images are referenced by absolute URLs.

---

## 2) How to customize

**Hero copy**

- Change the H1 and paragraph inside the `hero_text` block.
- Adjust hero height by editing `height: 160px` in the hero `<td>` **and** the Outlook VML `<v:rect>` height.

**Hero background image**

- Update both:
  - CSS `background-image: url('...')` on the hero `<td>`
  - `background="..."` attribute on the same `<td>`
  - `<v:fill ... src="...">` in the VML fallback (for Outlook).

**CTA button**

- Replace the `href` on the `<a class="btn">`.
- Inline styles keep a solid fallback + gradient for modern clients.

**Colors & typography**

- Primary type stack is set on elements with `.hero_title`, `.hero_sub`, `.email_body`, `.email_footer`, `.btn`.
- Light mode colors are inline/CSS; dark mode overrides live in `<style>`.

**Footer text**

- Update the legal line inside `.email_footer`.

---

## 3) Rendering techniques used

- **Table‑based layout** with `role="presentation"` to satisfy legacy clients.
- **Background image:** CSS for modern clients + **VML fallback** (`<v:rect>/<v:fill>`) for Outlook.
- **Bulletproof CTA:** Solid background (fallback) + linear‑gradient for modern clients.
- **Responsive:** Mobile media queries reduce paddings and type sizes ≤600px.
- **Dark mode support:**
  - `@media (prefers-color-scheme: dark)` for Apple Mail/desktop/mobile clients.
  - `[data-ogsc]` hooks for **Outlook.com** web dark mode.
  - Light backgrounds flip to dark, text colors flip to light; CTA text stays white.

---

## 4) Testing instructions

**Quick manual preview**

1. Open `index.html` in a browser for a quick visual check.
2. Send a real email:
   - Paste HTML into your ESP or send via Gmail/Outlook as raw HTML (using a test sender tool).
   - Test to: Gmail web (light/dark), Outlook.com web (light/dark), Apple Mail (light/dark), Outlook desktop (Win), Gmail iOS/Android.

**Recommended services**: Litmus.

**What to verify**

- Hero image appears behind text (and shows a dark overlay).
- CTA is visible and clickable; gradient in modern clients, solid in Outlook.
- Mobile: type and paddings scale down; no horizontal scroll.
- Dark mode: body, content panels, and text flip correctly.
- Outlook desktop: hero height matches VML height; no extra table spacing.

---

## 5) Dark mode details

- System dark mode rules:
  ```css
  @media (prefers-color-scheme: dark) {
    .body {
      background-color: #0e0e0e !important;
    }
    .email_bg,
    .email_container,
    .email_body,
    .email_footer {
      background-color: #0e0e0e !important;
    }
    .email_body,
    .email_footer {
      color: #eaeaea !important;
    }
    .footer_text {
      color: #b8b8b8 !important;
    }
    .btn {
      color: #ffffff !important;
    }
  }
  ```

---

## 6) Accessibility

- Real text over the hero (no text in images).
- Sufficient contrast in both modes.
- Tables marked with `role="presentation"` for screen readers.
- Link text is descriptive (“Get Started”).

---

## 7) Known limitations / notes

- Background images are **not** supported in some very old clients; a solid fallback color `#333` ensures readable text.
- Gradients are ignored by Outlook desktop; button gracefully falls back to the solid color.
- CSS inlining: critical styles are inline; media queries and dark‑mode rules must remain in the `<style>` block.

---

## 8) Credits

- Hero photo: Unsplash (for testing only). Replace with licensed/owned assets for production.
