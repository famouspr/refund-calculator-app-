# Refund Calculator (Public App)

A tiny, zero-backend calculator for non-refundable payment processor fees
(default **2.9% + $0.30**) that shows the **refund amount** for a given charge.
Perfect as a **Help Scout custom sidebar app** (Callback URL) or any other
support tool that can render a simple HTTPS page.

- ⚡ No build step (pure HTML/CSS/JS)
- 🧩 Two flavors: `full/` and `compact/`
- 🔧 Configurable via **URL params** (percent, flat fee, title, currency)
- 🌐 Host anywhere (Vercel recommended)

---

## Live structure

- **Full** UI: `full/index.html`  
- **Compact** UI: `compact/index.html` (ultra-small; designed to avoid internal scrolling)

> Both versions auto-calc: `fee = amount * (percent/100) + flat`;  
> `refund = amount - fee`. Results are rounded to 2 decimals.

---

## URL Parameters

| Param     | Type   | Default | Example                 | Notes                          |
|----------|--------|---------|-------------------------|--------------------------------|
| `pct`    | float  | 2.9     | `?pct=2.5`              | Processor percentage fee       |
| `flat`   | float  | 0.30    | `?flat=0.25`            | Flat fee in currency units     |
| `title`  | string | (full: “Refund Calculator”, compact: hidden) | `?title=My%20Refunds` | Optional heading (full only)  |
| `cur`    | string | `$`     | `?cur=£`                | Currency symbol override       |

**Examples**
- Full version with different fees:  
  `https://yourapp.vercel.app/full/?pct=2.7&flat=0.25&title=Refund%20Calculator`
- Compact version with GBP:  
  `https://yourapp.vercel.app/compact/?cur=£`

---

## Help Scout Integration (Callback URL)

1. In **Help Scout** → **Manage → Apps → Create → Create App**.
2. **Callback URL** = your deployed URL, e.g.  
   - Full: `https://yourapp.vercel.app/full/`  
   - Compact: `https://yourapp.vercel.app/compact/`
3. Choose mailboxes → **Save**. Open any conversation to see the app.

> Tip: The **compact** version is tuned to avoid internal scrolling in the sidebar.
> Use the **full** version if you want an internal title and slightly more spacing.

---

## Other Platforms (custom app via <iframe>)

Most help desks/crm tools let you embed an HTTPS URL as a sidebar panel.

```html
<iframe
  src="https://yourapp.vercel.app/compact/?pct=2.9&flat=0.30&cur=$"
  title="Refund Calculator"
  style="width:100%; border:0; height:200px;"
  loading="lazy"
></iframe>
