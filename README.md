# ByErim Shopify Theme — Fixes & Features
Maintained by BeBe 💜

---

## 🔧 Fix 1: Google Ads Enhanced Conversions

**Problem:** Google Ads flagged missing user data (name, postcode, country) on conversion events, reducing match accuracy and campaign optimisation.

**Fix:** Two snippets that pass customer data to Google Ads on the order confirmation page.

### Files
- `snippets/google-base-tag.liquid` — updated base tag with `allow_enhanced_conversions: true`
- `snippets/google-enhanced-conversions.liquid` — fires on thank you page, sends customer data

### Deployment Steps

#### Step 1 — Get your conversion label
1. Google Ads → Goals → Conversions
2. Click your Purchase conversion action
3. Go to **Tag setup** → **Use Google Tag Manager** → note the **Conversion label** (looks like `AbCdEfGhIjKlMnO`)
4. Open `snippets/google-enhanced-conversions.liquid` and replace `CONVERSION_LABEL_HERE` with it

#### Step 2 — Add snippets to theme
In Shopify Admin → Online Store → Themes → Edit code:

1. **Upload** `snippets/google-base-tag.liquid` and `snippets/google-enhanced-conversions.liquid` to the Snippets folder

2. **In `layout/theme.liquid`**, find `</head>` and add before it:
   ```liquid
   {% render 'google-base-tag' %}
   ```

3. **In `layout/theme.liquid`**, find `</body>` and add before it:
   ```liquid
   {% render 'google-enhanced-conversions' %}
   ```

#### Alternative: Quick deploy via Additional Scripts (no theme edit needed)
1. Shopify Admin → Settings → Checkout
2. Scroll to **Order status page** → Additional scripts
3. Paste the full contents of `snippets/google-enhanced-conversions.liquid` directly

> ⚠️ You still need to replace `CONVERSION_LABEL_HERE` before deploying

### What this fixes
- ✅ Enhanced conversions: missing address fields
- ✅ Enhanced conversions: no user-provided data found
- ✅ `allow_enhanced_conversions: true` flag on base tag

---

## 🚀 Coming Soon
- [ ] Hair Oil landing page (conversion-optimised, no nav)
- [ ] AI ad campaign tracking pixels
