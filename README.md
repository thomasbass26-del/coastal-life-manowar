# Man O' War & Pine Lakes — Golf Landing Page

The Coastal Life Team of Myrtle Beach · Coldwell Banker Sea Coast Advantage

Standalone site. Page lives at the domain root.

```
index.html
CNAME                        <- create this, one line, your domain
robots.txt
sitemap.xml
man-o-war-hero.mp4      11 MB   desktop hero loop, muted
man-o-war-hero-mobile.mp4 4.5 MB mobile hero loop, muted
man-o-war-film.mp4      25 MB   full film with audio, plays on click
img/poster.jpg                  hero still
img/og.jpg                      social share image
```

## Two placeholders to fill before this works

Search and replace across `index.html`, `robots.txt`, and `sitemap.xml`:

| Placeholder | Replace with |
|---|---|
| `DOMAIN_PLACEHOLDER` | the custom domain, no protocol, e.g. `coastallifemb.com` |
| `PASTE_COASTAL_LIFE_TEAM_ENDPOINT_HERE` | the Coastal Life Team's own Zapier catch hook |

Then set `live: true` in `CLT_CONFIG` at the top of `index.html`.

Until the endpoint is real the form runs in test mode: it validates, shows the
thank-you state, and logs the payload to the browser console instead of sending.
That is deliberate, so a half-configured page never silently drops a lead.

**The phone and email in `CLT_CONFIG` are placeholders too.** Replace them.

## Lead routing

This page posts to **the Coastal Life Team's own hook**, not the one used by the
Rivers Edge / Waterbridge / Sunset Harbour pages on livingcoastalsc.com. Those
route to a different team. Keep them separate.

Payload is form-encoded, `mode: 'no-cors'` (Zapier catch hooks send no CORS
headers, so the response is opaque and there is no status to check — a completed
request counts as success). Fields arriving at the Zap:

```
lead_source    man-o-war-pine-lakes-landing
team           coastal-life-team
first_name
last_name
email
phone
community      Pine Lakes | Man O' War | Both | Open
timeline       0-3 months | 3-6 months | 6-12 months | Researching
page           full URL including query string
referrer
utm_source utm_medium utm_campaign utm_content utm_term gclid fbclid
submitted_at   ISO-8601
```

Build the Zap against these keys. A hidden honeypot field blocks basic bots and
never reaches you.

## Video

The Dropbox original is a 4K master: 3840×2160, 50 Mbps, 485 MB, 1:20. It cannot
be served to visitors — nobody streams 50 Mbps, and Dropbox share links are
bandwidth-capped, so the video would silently die once the page got traffic.

The three files here are re-encodes: same footage, `faststart` enabled so playback
starts before the file finishes downloading. Hero sizes match the pattern already
used on the other CBSCA community pages (7–11 MB desktop, 4–5 MB mobile).

**Keep the 4K master somewhere safe.** It's the archive copy for future cuts, ads,
and MLS video.

### Bandwidth — worth watching

GitHub Pages has a soft limit around 100 GB/month and their terms say it isn't
meant to serve as a CDN or for primarily-video sites. Rough math per visitor:

| | Downloads |
|---|---|
| Desktop visitor | ~11 MB |
| Mobile visitor | ~4.5 MB |
| Anyone who clicks *Watch the film* | +25 MB |

A few thousand visits a month is fine. If this becomes a paid-traffic page, move
the three mp4s to Cloudflare R2 (free egress) or Bunny and point the `src` values
at that host — the HTML can stay on Pages. That's a ten-minute change, but do it
before the traffic arrives, not after Pages starts throttling.

## Before launch

- [ ] `DOMAIN_PLACEHOLDER` replaced everywhere (3 files)
- [ ] Zapier hook in, `live: true`
- [ ] Real team phone and email in `CLT_CONFIG`
- [ ] `CNAME` file created, DNS pointed at GitHub Pages
- [ ] Test submission lands in the Zap and reaches the CRM
- [ ] Official CB Sea Coast Advantage logo swapped in for the masthead text lockup
- [ ] The guide PDF exists and the Zap actually emails it — the form promises one
- [ ] Broker review of the footer disclosures

## Facts on the page

| | Pine Lakes | Man O' War |
|---|---|---|
| Opened | 1927 | 1996 |
| Architect | Robert White | Dan Maples |
| Par | 70 | 72 |
| Yards | 6,675 | 6,967 |
| Greens | Sunday ultradwarf bermuda | Crenshaw bentgrass |

Robert White was the first president of the PGA of America. *Sports Illustrated*
came out of a 1954 Time Inc. conference at Pine Lakes. Man O' War is believed to be
the only course in the world with back-to-back island greens (14 and 15), plus a
par-4 ninth on its own island.

Both clubs are public daily-fee and independently operated. The footer disclaims
any affiliation with the brokerage — implying club access comes with the house is
the kind of claim that causes problems. Verify yardage and par against each club's
current scorecard before print; courses re-rate.
