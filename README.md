# ByErim Shopify Theme — Fixes & Features
Maintained by BeBe 💜

---

## 🔧 Fix 1: Google Ads Enhanced Conversions

**Problem (from Google Ads alert):**
- "Enhanced conversions: missing address fields"
- "Enhanced conversions: no user-provided data found"

**Root cause:** The existing gtag setup doesn't pass customer data (name, email, postcode, country) to Google Ads after purchase. No conversion label needed — this fix enriches existing events.

### Files
| File | Purpose |
|------|---------|
| `snippets/google-base-tag.liquid` | Updated gtag with `allow_enhanced_conversions: true` |
| `snippets/google-enhanced-conversions.liquid` | Sets user_data on order confirmation page |

### Deploy — Quick (no theme edit, 2 mins)

1. Go to **Shopify Admin → Settings → Checkout**
2. Scroll to **Order status page** → **Additional scripts**
3. Paste the full contents of `snippets/google-enhanced-conversions.liquid`
4. Save

That's it. No conversion label required. Google de-dupes by `transaction_id`.

### Deploy — Full (theme edit, recommended)

In **Shopify Admin → Online Store → Themes → Edit code**:

1. Upload both files to the `snippets/` folder
2. In `layout/theme.liquid`, **replace** your existing `<script async src="https://www.googletagmanager.com/gtag/js..."` block with:
   ```liquid
   {% render 'google-base-tag' %}
   ```
3. Before `</body>`, add:
   ```liquid
   {% render 'google-enhanced-conversions' %}
   ```
4. Save and publish

### What this fixes
- ✅ Enhanced conversions: no user-provided data found
- ✅ Enhanced conversions: missing first name, surname, postcode, country
- ✅ `allow_enhanced_conversions: true` flag on base tag
- ✅ Safe deduplication via transaction_id (won't double-count orders)

---

## 🚀 Coming Soon
- [ ] Hair Oil — conversion-optimised landing page (no nav, single CTA)
- [ ] Meta Pixel enhanced conversions
- [ ] TikTok Pixel server-side events
