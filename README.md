---
title: "Remote Monitoring - Collaboration Guide"
description: "Contributing guide for the Remote Monitoring blog series"
tableOfContents: true
sidebar:
  order: 999
---

# Remote Monitoring

![Build](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Contributors Welcome](https://img.shields.io/badge/contributors-welcome-orange)

**Read this series at:** [https://siliconwit.com/blog/remote-monitoring/](https://siliconwit.com/blog/remote-monitoring/)

A post-per-installation series on what connected equipment actually tells you. Each post takes one live device from the SiliconWit public reference fleet, reads its charts properly, works the arithmetic, and asks what catching that fault early is worth. Every figure quoted in a post is derived from that device's own readings, never illustrative.

## Posts

| # | Post | Installation | Angle |
|---|------|--------------|-------|
| 1 | [Cold Store Monitoring](https://siliconwit.com/blog/remote-monitoring/cold-store-seafood/) | [Cold store, seafood processing](https://siliconwit.io/d/cold-store-seafood) | The compliance record, and duty as the early warning |
| 2 | [The Pump That Ran Dry](https://siliconwit.com/blog/remote-monitoring/borehole-and-storage-tank/) | [Borehole and storage tank](https://siliconwit.io/d/borehole-and-storage-tank) | Incident post-mortem |
| 3 | [Never Off, Still a Shift Short](https://siliconwit.com/blog/remote-monitoring/cnc-machine-tool/) | [CNC machine tool](https://siliconwit.io/d/cnc-machine-tool) | Utilisation economics and quoting |
| 4 | [The Alarm That Fires Every Night](https://siliconwit.com/blog/remote-monitoring/greenhouse-cut-flowers/) | [Greenhouse, cut flowers](https://siliconwit.io/d/greenhouse-cut-flowers) | Threshold placement and alert fatigue |
| 5 | [Forty Litres, Engine Stopped](https://siliconwit.com/blog/remote-monitoring/off-grid-tower-solar-genset/) | [Off-grid tower site](https://siliconwit.io/d/off-grid-tower-solar-genset) | Fuel reconciliation |
| 6 | [Fans on a Timer, or on a Reading](https://siliconwit.com/blog/remote-monitoring/car-park-co-monitoring/) | [Car park carbon monoxide](https://siliconwit.io/d/car-park-co-monitoring) | Demand-driven ventilation |
| 7 | [The Excursion Nobody Saw](https://siliconwit.com/blog/remote-monitoring/laboratory-incubator/) | [Laboratory incubator](https://siliconwit.io/d/laboratory-incubator) | Data integrity |
| 8 | [Thirty Outages Nobody Logged](https://siliconwit.com/blog/remote-monitoring/building-power-monitoring/) | [Building power monitoring](https://siliconwit.io/d/building-power-monitoring) | Frequency against duration |
| 9 | [Built by a Class, Left Public](https://siliconwit.com/blog/remote-monitoring/student-weather-station/) | [Student weather station](https://siliconwit.io/d/student-weather-station) | A reading against a measurement |

Every installation above is on the [public device gallery](https://siliconwit.io/public-devices), open with no account.

One post per industry category, each with its own angle. The fleet has only about eight distinct sensor templates behind its devices, so a shared instrument set is normal and the angle is what keeps the series from repeating itself.

## File Structure

```
remote-monitoring/
├── index.mdx
├── cold-store-seafood.mdx
├── borehole-and-storage-tank.mdx
├── cnc-machine-tool.mdx
├── greenhouse-cut-flowers.mdx
├── off-grid-tower-solar-genset.mdx
├── car-park-co-monitoring.mdx
├── laboratory-incubator.mdx
├── building-power-monitoring.mdx
├── student-weather-station.mdx
├── images/
│   ├── availability-arithmetic.svg
│   ├── compressor-duty-headroom.svg
│   ├── excursion-and-the-run.svg
│   ├── fuel-reconciliation.svg
│   ├── pm-subset-and-ratio.svg
│   ├── pump-current-and-flow.svg
│   ├── threshold-placement.svg
│   ├── timer-versus-demand.svg
│   └── utilisation-arithmetic.svg
├── LICENSE
└── README.md
```

Explanatory figures live in `images/` in this repository. Chart images and hero images do not: charts are generated into `public/device-plots/` in the main site repository, and heroes are served from `cdn.siliconwit.com/blog/remote-monitoring/`.

## Where the Numbers Come From

Every figure in a post comes from the readings of the installation it is about. Charts are rendered by `scripts/generate-device-plots.py` in the main site repository:

```bash
# default: the trailing three days
python3 scripts/generate-device-plots.py cold-store-seafood

# a window anchored on a logged incident, with explicit fields per chart
python3 scripts/generate-device-plots.py borehole-and-storage-tank \
    --incident 1 --days 1.5 --suffix dry-run \
    --fields "tank_level_pct,pump_duty_pct|motor_current_a"
```

The rendered PNGs are committed to the main repository rather than fetched at page render. An installation can be retired or made private, and a post from 2026 still has to draw its charts in 2029. The image is the record; the link to the live device is a courtesy on top of it.

## How to Contribute

All commands below work on Linux, macOS, and Windows (using Git Bash, PowerShell, or Command Prompt with Git installed).

### For Team Members (with push access)

**First time setup (clone the repo once):**

```bash
git clone https://github.com/SiliconWit/remote-monitoring.git
cd remote-monitoring
```

**Every time you start working:**

```bash
git pull origin main
```

Always pull before making changes. This avoids conflicts with other contributors.

**After making your changes:**

```bash
git add .
git commit -m "Brief description of what you changed"
git push origin main
```

**If you get a push error** (someone pushed before you):

```bash
git pull origin main
```

Git will merge the changes automatically in most cases. If there is a conflict, Git will mark the conflicting lines in the file. Open the file, choose which version to keep, then:

```bash
git add .
git commit -m "Resolve merge conflict"
git push origin main
```

**Tips to avoid conflicts:**

- Always `git pull origin main` before you start working
- Push your changes as soon as you are done, do not hold onto uncommitted work for long
- Coordinate with other contributors so two people are not editing the same file at the same time

### For External Contributors (without push access)

1. Fork the repository: [SiliconWit/remote-monitoring](https://github.com/SiliconWit/remote-monitoring)
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR-USERNAME/remote-monitoring.git
   cd remote-monitoring
   ```
3. Make your changes and commit:
   ```bash
   git add .
   git commit -m "Brief description of what you changed"
   git push origin main
   ```
4. Open a Pull Request against `main` on the original repository
5. Describe what you changed and why in the PR description

## Content Standards

- All post files use `.mdx` format
- Do not use `<BionicText>` in this series
- No em dashes or en dashes anywhere in the prose
- **Every number must be re-derivable from the installation's own readings.** If a figure cannot be recomputed from them, it does not belong in a post
- Calculations are shown as worked LaTeX, not asserted. The site renders MathJax, so use `$$...$$` with `\text{}` for units and `{,}` for thousands separators:
  ````mdx
  $$\text{utilisation} = \frac{63.7\ \text{h}}{72.3\ \text{h}} = 88.1\%$$
  ````
- Never write a bare `$` in prose. It opens a math span and breaks the page. Write currency as `USD 72,000`
- Charts must be regenerated whenever the numbers quoted around them change, so image and prose always agree
- Explanatory figures are SVG, white background, Arial, two panels labelled `(a)` and `(b)`, matching the derivation figures in the mechanics-of-materials course
- Image alt text describes what each panel shows, not just the title
- One angle per post. Check the table above before writing so a new post does not repeat an existing one
- Hero images are 800x520 SVG rendered to PNG, kept under 100 KB, and carry their `siwit.co` short code
- Publication dates go backwards from the present, at most two in any seven-day window, and never in the future

## Local Development

To preview the full site locally, clone the main site repository and initialize submodules:

```bash
git clone --recurse-submodules <main-repo-url>
cd siliconwit-com
npm install
npm run dev
```

To test a production build:

```bash
npm run build
```

## License

This content is released under the [MIT License](LICENSE).
