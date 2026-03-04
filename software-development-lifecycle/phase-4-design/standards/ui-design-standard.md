# UI Design Standard

| Field | Value |
|-------|-------|
| **Standard ID** | STD-P4-004 |
| **Compliance Level** | Mandatory |
| **Enforced By** | Tech Lead |
| **Verification Method** | Design Review |
| **Last Verified** | 2026-03-04 |

---

## SCALING GATE

> **IF** small project (1-2 devs) **THEN** Responsive breakpoints, accessibility contrast/keyboard, form validation required; RTL support deferred if English-only
> **IF** medium project (3-5 devs) **THEN** Full compliance; WCAG audit may use automated tools only
> **IF** large project (6+ devs) **THEN** Full compliance required including manual WCAG audit

---

## COMPLIANCE REQUIREMENTS

### Responsive Design

| Breakpoint | Min Width | Target |
|-----------|-----------|--------|
| Mobile | 320px | Smartphones |
| Tablet | 768px | Tablets, small laptops |
| Desktop | 1024px | Standard laptops, desktops |
| Large Desktop | 1440px | Large monitors |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 1 | Mobile-first design: start with mobile layout, expand for larger screens | All pages | [ ] Mobile layout verified at 320px | Block deployment |
| 2 | All 4 breakpoints supported (320px, 768px, 1024px, 1440px) | All pages | [ ] Each breakpoint tested | Block deployment |

### RTL/LTR Support

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 3 | Use CSS logical properties (margin-inline-start, not margin-left) | All layout CSS | [ ] No physical direction properties | Reject PR |
| 4 | Text alignment uses start/end, not left/right | All text alignment | [ ] Alignment properties audited | Reject PR |
| 5 | Directional icons (arrows, progress) mirrored in RTL | All directional icons | [ ] RTL icon rendering verified | Reject PR |
| 6 | Numbers displayed LTR even in Arabic text | All numeric displays | [ ] Number direction verified in Arabic | Reject PR |
| 7 | Date format: Arabic locale dd/mm/yyyy, English locale yyyy-mm-dd | All date displays | [ ] Date format per locale verified | Reject PR |
| 8 | Language switcher on every page, persists user preference | All pages | [ ] Switcher present and functional | Block deployment |

### Accessibility (WCAG 2.1 AA)

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 9 | Color contrast minimum 4.5:1 for normal text, 3:1 for large text | All text | [ ] Contrast ratio tested | Block deployment |
| 10 | All interactive elements reachable via Tab; focus order matches visual order | All interactive elements | [ ] Keyboard navigation tested | Block deployment |
| 11 | All images have alt text; form fields have labels; ARIA roles for custom components | All images, forms, custom components | [ ] Screen reader audit | Block deployment |
| 12 | Visible focus ring on all focusable elements; never remove outline without replacement | All focusable elements | [ ] Focus indicators visible | Block deployment |
| 13 | Errors identified by text, not color alone; error messages adjacent to field | All error states | [ ] Error identification verified | Block deployment |
| 14 | Content remains usable at 200% zoom | All pages | [ ] 200% zoom test passed | Block deployment |

### Form Design

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 15 | Every field has visible label above field; no placeholder-as-label | All form fields | [ ] Labels present and visible | Reject PR |
| 16 | Required fields marked with asterisk (*) and "Required" in screen reader text | All required fields | [ ] Required indicators present | Reject PR |
| 17 | Validate on blur; show inline error below field | All validated fields | [ ] Blur validation tested | Reject PR |
| 18 | Error messages are specific (e.g., "Email must be in format name@domain.com") | All error messages | [ ] Error message specificity reviewed | Reject PR |
| 19 | Submit button disabled until all required fields valid; loading state during submission | All forms | [ ] Button state behavior verified | Reject PR |
| 20 | Success feedback via toast notification or redirect | All form submissions | [ ] Success feedback present | Reject PR |

### Component States

Every UI component must handle:

| State | Implementation |
|-------|---------------|
| Loading | Skeleton loader or spinner; never blank page |
| Empty | Helpful message with action suggestion |
| Error | Error message with retry option; log to console |
| Success | Toast notification, auto-dismiss after 5 seconds |
| Partial | Show available data; show error for failed sections |

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 21 | Loading state uses skeleton loader or spinner (no blank pages) | All data-fetching components | [ ] Loading state present | Reject PR |
| 22 | Empty state shows helpful message with action suggestion | All list/data components | [ ] Empty state message present | Reject PR |
| 23 | Error state shows message with retry option | All data-fetching components | [ ] Error state with retry present | Reject PR |
| 24 | Success state uses toast notification, auto-dismiss 5 seconds | All action components | [ ] Toast behavior verified | Reject PR |
| 25 | Partial failure shows available data with error for failed sections | All composite components | [ ] Partial state handled | Reject PR |

### Navigation

| # | Rule | Applies To | Verification | Violation Response |
|---|------|-----------|-------------|-------------------|
| 26 | Primary nav: sidebar (desktop) or hamburger menu (mobile); max 8 top-level items | All pages | [ ] Nav structure verified | Reject PR |
| 27 | Breadcrumbs required for pages more than 2 levels deep | Deep pages | [ ] Breadcrumbs present | Reject PR |
| 28 | Current page highlighted in navigation | All pages | [ ] Active state visible | Reject PR |
| 29 | Every page has unique, descriptive title (browser tab) | All pages | [ ] Page titles unique and descriptive | Reject PR |
| 30 | Browser back button works correctly on all pages | All pages | [ ] Back navigation tested | Reject PR |

---

## COMPLIANCE CHECKLIST

- [ ] Mobile-first design with all 4 breakpoints supported
- [ ] CSS uses logical properties (no physical left/right)
- [ ] RTL layout, icons, numbers, and dates verified
- [ ] Language switcher present on every page
- [ ] Color contrast meets WCAG 2.1 AA (4.5:1 normal, 3:1 large)
- [ ] All interactive elements keyboard-accessible with correct focus order
- [ ] All images have alt text; forms have labels; custom components have ARIA roles
- [ ] Visible focus indicators on all focusable elements
- [ ] Errors identified by text, not color alone
- [ ] Content usable at 200% zoom
- [ ] All form fields have visible labels (not placeholder-as-label)
- [ ] Required fields marked; validation on blur; specific error messages
- [ ] Submit button disabled until valid; loading state during submission
- [ ] All 5 component states handled (loading, empty, error, success, partial)
- [ ] Navigation: sidebar/hamburger, breadcrumbs, active state, unique titles, back button

---

## CROSS-REFERENCES

| Document | Type | Link |
|----------|------|------|
| Create Detailed Design | Runbook | ../runbooks/create-detailed-design.md |
| Conduct Design Review | Runbook | ../runbooks/conduct-design-review.md |
| Design Review Checklist | Template | ../templates/design-review-checklist.md |
