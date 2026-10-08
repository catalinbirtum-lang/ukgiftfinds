# Image licensing rules: UK Gift Finds (in force from 8 October 2026)

Every image or video file published on this site must be one of the three permitted kinds below. If it isn't, the product gets our own text card instead. These rules apply to the site, the daily top-20 build, the catalogue, the TikTok landing page, Pinterest pins and unposted video assets.

## Permitted sources
1. **(a) Amazon Associates tools.** Image URLs returned by the Product Advertising API (or its successor), or SiteStripe image links, used **unmodified** and **together with the tagged affiliate link** (`tag=ukgiftfinds-21`), following that tool's display and caching rules. We have no API access yet (it needs qualifying sales), so we use none of these today. Never download, crop, cut out, re-host or burn Amazon listing images into pins or videos.
2. **(b) Brand-press or retailer-kit images**, but only where the brand's **published terms explicitly allow reuse** for our kind of use (commercial or affiliate promotion). Record the terms URL and the exact quote in the register before using any such image. "It's on the brand's own website" is **not** permission.
3. **(c) Our own original graphics** with no third-party product imagery: text cards from `engine/scripts/imglicence.py` (PNG marker `UKGF-Origin: own-text-card-v1`) and code-drawn illustrations with no logos or packaging (for example the `/picks/` heroes).

## Not permitted
- Photos taken from brand websites, Shopify stores, press pages or media servers without explicit reuse terms. This includes every image the daily build used before 8 October 2026.
- Amazon listing images obtained in any other way (scraped, saved, cut out or edited), including brand-hosted copies of them.
- Reseller, marketplace, mirror, competitor or social-media images and other creators' footage.
- AI edits of a real product photo for revenue content. FLUX-Kontext-style edits are a licence grey area.

## How it's enforced
- **Register:** `engine/IMAGE_LICENCE_REGISTER.csv` (sha256, status, source type, source URL, terms URL, terms quote, who checked it, date). Only rows with status `PERMITTED` count.
- **Builders:** `growth/daily20/scripts/make_pins.py`, `build_top20.py`, `engine/catalog/build_catalog.py` and `growth/tiktok_landing/build_tiktok_page.py` use a source image only if it's registered. Otherwise they draw our own text card or panel.
- **Publish gate:** `ukgiftfinds/publish_pages.sh` runs `engine/scripts/imglicence.py check` and **refuses to publish** if any image or video file is unregistered and unmarked, or if any page hotlinks an external image.
- **Videos:** unposted video assets that use unlicensed imagery go into the private `_unlicensed/` folder (never published) and come out of every queue. Posted TikTok videos are **never deleted** by us. They're listed for Catalin to decide.
- **Adding an image:** check the source against (a), (b) or (c), add a register row with evidence, then rebuild. If in doubt, use a text card.
