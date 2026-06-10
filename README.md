# Radio Midnight 📻

**Radio from round midnight, round the world 🌍**

**Live site:** [joelucadooley.github.io/radio-midnight](https://joelucadooley.github.io/radio-midnight)

[![Sponsor on GitHub](https://img.shields.io/badge/Sponsor%20on-GitHub-black?logo=github&style=for-the-badge)](https://github.com/joelucadooley)
[![Support me on Ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/joelucadooley)

Radio Midnight is always tuned to wherever on Earth it's currently around midnight. Solar midnight is a single line of longitude that sweeps westward around the planet at 15° per hour, and the player follows it — hopping from station to station, country to country, east to west, completing a full lap of the globe every 24 hours. Press one button and drift.

---

## How it works

1. The player computes the **midnight meridian** — the longitude where it's solar midnight right now — directly from UTC time. No timezone tables, just the sun.
2. It queries the community-run [Radio Browser](https://www.radio-browser.info/) database for stations in the country under the line, sorted east to west by each station's real coordinates.
3. Each station plays for **~45 seconds**. A few seconds before the switch, the next station is connected and buffered silently in the background on a second audio player.
4. The two streams then **equal-power crossfade** (~0.5s), so there's never a gap and never a long overlap. Dead streams are skipped silently while the current one keeps playing.
5. When a country's stations run out, the player steps west to the next country, chasing midnight forever.

The whole thing is a single static HTML file. No build step, no backend, no accounts, no cost.

## The map

The world map scrolls beneath a fixed, glowing **00:00** meridian pinned at centre screen — the planet turns, midnight stays still. The warm dot is the station you're hearing, plotted from its actual coordinates. Coastlines are [Natural Earth](https://www.naturalearthdata.com/) 1:110m land polygons, fetched at runtime and rendered as a single SVG path, with a graticule fallback if the data can't load.

## Constraints worth knowing

- Browsers only allow **HTTPS** streams on a secure page, so the player draws from the HTTPS slice of the Radio Browser database. Some regions are sparser than others.
- Stream URLs are community-submitted and stations go offline; the player tests each stream muted before it's ever heard and quietly moves on from dead ones.
- "Around midnight" is honest to within a country's width — the player favours stations near the line and walks west through them, but coverage is uneven across the globe.

## Tech stack

- Vanilla HTML / CSS / JavaScript — one file, zero dependencies
- [Radio Browser](https://www.radio-browser.info/) for the worldwide station database
- [Natural Earth](https://www.naturalearthdata.com/) (via [martynafford/natural-earth-geojson](https://github.com/martynafford/natural-earth-geojson)) for coastlines
- [GitHub Pages](https://pages.github.com/) for hosting
- Fonts: [Instrument Serif](https://fonts.google.com/specimen/Instrument+Serif) and [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono)

## Project structure

```
radio-midnight/
└── index.html      # The entire app: styles, map, audio engine, station logic
```

That's it. That's the project.

## Running locally

No install, no build:

```bash
git clone https://github.com/joelucadooley/radio-midnight
cd radio-midnight
python3 -m http.server     # or any static server
```

Then open `http://localhost:8000`. (Opening the file directly also works in most browsers, but a local server matches how it behaves on GitHub Pages.)

---

Created by [Joe Luca Dooley](https://github.com/joelucadooley) · Open source · Made for the night owls 🌙
