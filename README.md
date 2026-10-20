# SELENE — Watch the Earth rise

A one-page concept site for a fictional lunar expedition company. The hero is
six photographic layers cut from one render, stacked and pinned: scroll clears
a veil of cosmic dust, the Earth climbs out from behind the lunar horizon
under a tracked `EARTHRISE` title, and the crater rim closes in around an
astronaut on a rock. Below: the Earth → Moon flight drawn leg by leg as you
scroll, a mission-log reel that keeps the centre frame in focus, mission
cards with orbit rings, and a waitlist beside a live launch-window countdown.

## Stack

- Vite 6 + React 19 + TypeScript (`npm run lint` = `tsc --noEmit`)
- Tailwind CSS v4 via `@tailwindcss/vite` — no `tailwind.config.js`; the
  theme lives in the `@theme` block in `src/index.css`
- Lenis smooth scrolling driven by the page's **single rAF loop** — no GSAP,
  no Motion; every scroll beat is plain arithmetic on scroll progress, and
  nothing goes through React state while scrolling
- Michroma (display) / Manrope (text) / IBM Plex Mono (telemetry) from
  Google Fonts via `<link>`

## Run

```bash
npm install        # on machines where npm is configured with omit=dev, use:
                   #   NODE_ENV=development npm install --include=dev
npm run dev        # http://localhost:3006
npm run lint       # tsc --noEmit
npm run build      # production build → dist/
```

All 17 image assets (~2.7 MB: hero layers in `d`/`m` cuts, mission-log stills,
`og.jpg`) are committed under `public/` — nothing is hotlinked.

## Structure

```
src/lib/scroll.ts    one rAF loop for the page (Lenis + onFrame subscribers)
src/lib/math.ts      clamp / lerp / range / pinProgress helpers
src/components/      Earthrise (6-layer pinned hero), MissionLog (reel),
                     Trajectory (drawn flight path), Missions, Reserve, Chrome
src/hooks/           useReducedMotion, useReveals, useFitText
src/content.ts       every word on the page — swap copy here
public/layers/       hero layers, d (desktop) and m (mobile) cuts
public/media/        mission-log stills + og.jpg
```

## Notes

- All names, dates and missions are illustrative placeholders for a concept
  brand — the page says so itself. Replace `src/content.ts` before shipping.
- The waitlist form composes a `mailto:` draft; there is no backend.
- Accessibility: `aria-label`s, reduced-motion branches, and `prefers-reduced-motion`
  handling (Lenis disabled, dust stops drifting) are all wired in — keep them.
