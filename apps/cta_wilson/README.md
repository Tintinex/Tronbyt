# CTA Wilson Trains

A [Tronbyt](https://github.com/tronbyt) / Tidbyt app that shows live **CTA Train Tracker**
arrival times for the **Red** and **Purple** lines at the **Wilson** stop in Chicago.

![64x32 pixel display showing a "WILSON" header and the next Red/Purple line arrivals]

## What it shows

A header (`WILSON`, with red + purple swatches) followed by the next few arrivals.
Each arrival row has:

- a colored route badge (**R** = Red, **P** = Purple),
- the destination (e.g. `Howard`, `95th`, `Linden`, `Loop`),
- a countdown (`5m`, `Due`, or `Dly` for a delayed train).

## Setup

1. **Get a free CTA API key.** Request a CTA Train Tracker API key here:
   <https://www.transitchicago.com/developers/traintrackerapply/>
   (Approval is usually quick.)
2. **Add the app to your Tronbyt server** and open its configuration.
3. Paste your key into **CTA API Key**.
4. Optionally use **Lines** to limit the display to just Red or just Purple
   (default shows both).

## How it works

The app calls the CTA Train Tracker `ttarrivals` endpoint for the Wilson station:

```
https://lapi.transitchicago.com/api/1.0/ttarrivals.aspx?key=YOUR_KEY&mapid=41200&max=10&outputType=JSON
```

- `mapid=41200` is the Wilson station map ID (covers both Red and Purple platforms).
- Responses are cached for ~20s to stay well under the CTA rate limit.
- Times come back in `America/Chicago` and are turned into minute countdowns.

## Files

- `cta_wilson.star` — the Pixlet/Starlark app.
- `manifest.yaml` — app metadata for the Tronbyt/Tidbyt app catalog.

## Notes

- Wilson is served only by the Red and Purple lines, so no other routes appear.
- If you see `Set CTA API key`, the key field is empty.
- If you see `CTA error`, the key is likely invalid or not yet activated.
