# MediaRide homepage: V3 and V4 handoff

These are two new versions of the homepage, built from the client's two voice notes: one on the offer and ICP, one on the website.
The current homepage (`index.html`, V2) has not been touched.

| Version | File | Live link | Closing section |
|---|---|---|---|
| V3 | `home-v3.html` | https://mediaride-site.vercel.app/home-v3.html | Videos sliding past in two straight rows, one above the heading and one below (what the client asked for) |
| V4 | `home-v4.html` | https://mediaride-site.vercel.app/home-v4.html | The original arch of rotating videos from V2, kept for comparison |

V3 and V4 are otherwise identical. **Every change needs to go into both files.**

## Page order

1. **Hero:** the reel intro, with the headline "Every shoot, Built to perform." The tiles come in mixed sizes.
2. **Stats:** "Video that drives real impact". Each of the four stats opens a case study drawer.
3. **About:** the client's statement, with greyed "Trusted by" logos scrolling underneath. They don't pause on hover.
4. **One shoot, a month of content.** This section has no label.
5. **Services:** "Event coverage, stories and monthly video". Three big blocks:
   - Event coverage built for social
   - Go to market stories
   - Monthly video support
6. **What sets us apart:** a four-card bento.
   - We plan before we film. A Notion-style plan for "Acme DevCon", a made-up client, cycling Board, Script, Shoot and Edit.
   - Trusted by GTM teams. Glass logo pills over a video.
   - One crew, start to finish.
   - We know what marketing teams need.
7. **Testimonials:**
   - The video plays muted by itself, with a sound button.
   - The quote has a fixed four-line height, with the stat underneath.
   - Photos with a progress ring move to the next story when the clip ends.
8. **Closing section:** straight rows in V3, the arch in V4.
9. **Footer:** site map and socials on the left, then email and phone, then the big MediaRide wordmark inside the container.

## Client feedback covered

- The site isn't built around one ICP. No role-specific copy (CMO, VP, etc.) and no launch videos anywhere.
- Stats moved up and lead with impact, and each one is clickable into a case study.
- The About subtext became the main statement. The client's own line was lightly edited, and "launches" was removed.
- The staggered blocks and the problem section ("Sound familiar", "stuck on a drive") are removed.
- The four nuances are now visual cards. "Why us over another crew" is gone.
- Flat, blocky style with no gradients or glows. The one soft touch is the subtle glass on the logo pills.
- Dark grey `#292929` replaces black throughout. `#000` remains only in masks.
- The closing section and the footer follow the client's notes.

## Open items: waiting on the client

All of these are clearly marked placeholders in the code.

- **Case study drawers:** challenge, what we shot and results for all four stats.
  - Content lives in the `CASES` array in the script, searchable as `const CASES=`.
  - The clips used are stand-ins from the reel library.
- **Testimonials:**
  - The real quotes for Hook, Docker and Hanke & Apolonio go in the `T` array (`const T=[`).
  - Docker's and Hanke & Apolonio's videos are stand-ins.
  - The photos in `PEOPLE` are stand-ins. They're labelled only with the company name and "Client story" until the client confirms who said what.
- **Copy sign-off:** the headline, the About statement and the service blurbs. The client said they'd want to polish these.

## Decisions that differ from the client's notes

- **The reel intro stays.** The client floated cutting it. We kept it; worth asking them once they've seen V3.
- **Testimonials:** the client asked for written reviews with bigger faces. The page uses photos with a progress ring and no review cards (our call), so tell the client.
- **Service name:** the first service is still titled "Event coverage, built for social". That's the client's own name for it, though they were also worried about leaning on social.

## Small loose ends

- In the top nav, "About" and "Portfolio" link to `#`. About could point to `#about`, and there's no portfolio page yet.
- "See the work" in the hero goes to the services section, not to examples of work.
- The footer "Process" link goes to "One shoot, a month of content".

## Technical notes

- **Setup:**
  - Static HTML with inline CSS and JS, using GSAP 3.12.5 with ScrollTrigger and Lenis 1.1.13.
  - There's no doctype, so the page renders in quirks mode and `body` is the scroller. Lenis is patched to use `document.scrollingElement`.
- **Scaling:** between 901 and 1439px wide, the whole page is scaled with `zoom = innerWidth / 1440` on `<html>`. Anything that follows the mouse has to divide by that zoom: the custom cursor does `translate(x / Z)`.
- **Custom cursor (`#cur`):**
  - States:
    - `dot`: an inverted dot
    - `link`: an orange circle on text links and clear buttons
    - `cur-solid`: a 52px inverting disc on filled buttons, including the footer Subscribe button
    - `disc`: a labelled disc on the reel, the testimonial video and the stat cards
    - `txt`: a text caret in fields
  - **Gotcha:** the button state was once called `ring`, and V4's arch has its own `.ring` style. The cursor picked that style up and jumped off screen on V4. Keep cursor state names unique.
- **CSS order:** new style blocks were added after the line `@media (max-width:599px){.ws .ws-c3{height:270px}}`, so later rounds sit above earlier ones in the file. A few rules use extra specificity because of this.
- **Mobile:** breakpoints are at 900px and 599px, plus a tablet band from 600 to 900px. Everything was checked at 390px and 768px.

## Deploying

The site is the `mediaride-site` project on Vercel (team: compass-design-co).

```
vercel deploy --prod --yes --scope compass-design-co
```

Deploying publishes everything in the folder, including `index.html`. Make sure `index.html` is what you want live before you run it.
