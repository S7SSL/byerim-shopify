# ByErim SEO Fixes — Action List for James

**Priority: HIGH — these are blocking page 1 rankings**

---

## Fix 1 — Canonical Tag (CRITICAL)

**Problem:** `/collections/hair-oil` has canonical pointing to the product page. Google won't rank the collection.

**Fix:** In `theme.liquid`:
1. Find the existing `<link rel="canonical" ...>` tag and **DELETE IT** entirely
2. In its place, add:
```liquid
{% render 'seo-canonical-fix' %}
```
⚠️ Do NOT leave both — two canonical tags means Google ignores both.

Snippet file: `snippets/seo-canonical-fix.liquid` ✅

---

## Fix 2 — Homepage H1 (HIGH)

**Problem:** Homepage H1 reads "Stories from our Community" — Google thinks the page is about community stories.

**Fix:** In the homepage hero section (likely `sections/main-homepage.liquid` or similar):
1. Add this at the very top of the section:
```liquid
{% render 'seo-homepage-h1' %}
```
2. Find the existing `<h1>` tag(s) on the homepage and change them to `<h2>`

⚠️ A page should have exactly ONE H1. Adding this without demoting the existing H1 will hurt rankings.

Snippet file: `snippets/seo-homepage-h1.liquid` ✅

---

## Fix 3 — Ayurvedic Hair Oil Collection (HIGH)

**Problem:** No dedicated page targeting "ayurvedic hair oil" — a high-intent UK search term.

**Steps:**
1. Create new collection in Shopify Admin:
   - Title: `Ayurvedic Hair Oil`
   - Handle: `ayurvedic-hair-oil`
   - SEO title: `Ayurvedic Hair Oil UK | Natural & Vegan | ByErim`
   - SEO description: `Discover ByErim's award-winning Ayurvedic hair oil. 100% natural, vegan, and rooted in ancient Ayurvedic tradition. UK made. Free delivery over £30.`
2. Add products: Luxury Hair Oil, Hair Dew Duo, Hair Growth Kit
3. Render SEO content block in collection template:
```liquid
{% render 'seo-ayurvedic-collection' %}
```
Snippet file: `snippets/seo-ayurvedic-collection.liquid` ✅

---

## Fix 4 — Google Search Console Access

Grant `marge@byerim.com` Owner access in Search Console → enables BeBe to monitor rankings.

**URL:** https://search.google.com/search-console/users?resource_id=sc-domain:byerim.com

*(Sat has already added the user — pending Search Console API enablement in GCP)*

---

## Summary

| Fix | File | Effort |
|-----|------|--------|
| Canonical tag | snippets/seo-canonical-fix.liquid | 10 min |
| Homepage H1 | snippets/seo-homepage-h1.liquid | 10 min |
| Ayurvedic collection | snippets/seo-ayurvedic-collection.liquid | 20 min |
| Search Console | GCP console | 2 min |

Expected impact: collection pages indexable + homepage keyword relevance within 2–4 weeks.
