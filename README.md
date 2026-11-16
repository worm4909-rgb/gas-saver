# Gas nearby

A small web app that lists gas stations near you, compares prices, and works out which one is cheapest for your car. It is a single page (`index.html`) with no build step.

## What it does

- Lists nearby stations with prices for regular, midgrade, premium and diesel
- Distance slider and a Leaflet map with OpenStreetMap tiles
- Radar sweep on the map that makes each station "ping" and light up as the line passes it (can be switched off with the Radar button)
- Tap the map to see it full screen; tap a station in full screen for its price and a Google Maps directions link
- "Your car" box: tank size, miles per gallon and tank level, so it can work out the total cost to fill up, including the gas used to drive there and back
- Per-station discount slider (rewards cards, memberships)
- Confidence badge on every price (high, medium, low)
- "Prices near you" box, color coded against the state average
- Settings button to change the page color
- Gas pump app icon, so it looks right when added to a phone's home screen
- You can type in a price you see at the pump; it is saved in your browser

## Run it on your computer

Double-click `index.html`. It needs an internet connection for the map, fonts and the Leaflet library.

## Put it on GitHub and get a link (GitHub Pages)

1. On github.com, click **New repository**, name it (for example `gas-nearby`), keep it public, and create it.
2. Click **uploading an existing file**, drag in everything from this folder (all the files, including the icon images), and click **Commit changes**.
3. Go to **Settings**, then **Pages**. Under "Build and deployment", choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute or two your app is at `https://YOUR-USERNAME.github.io/gas-nearby/`.

## Add it to your phone's home screen

Open your GitHub Pages link on your phone. On iPhone, tap Share, then **Add to Home Screen**. On Android, open the browser menu and tap **Add to Home screen** or **Install app**. It shows the gas pump icon. The icon files are `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` and `favicon-32.png`, and `manifest.webmanifest` tells the phone the app's name and colors. This is a web shortcut, not an app from an app store.

## Change the data

Everything is in `index.html`. Search for `const S=[` to find the stations. Each one looks like this:

```js
{id:1,name:"Shell",addr:"507 N 3rd St",mi:1,ang:20,p:[4.00,4.19,4.39,3.99],unv:1,src:"an online business directory (date unknown)"}
```

- `p` is the price for regular, midgrade, premium and diesel. Use `null` for a price you don't have.
- `mi` is the distance from you in miles.
- `unv:1` marks a price as unverified (low confidence). Remove it for a price you trust, and change `src` to say where it came from.
- `ll:[lat,lng]` is optional. Add exact coordinates to put the pin in the right spot. Right-click a spot in OpenStreetMap or Google Maps to copy its coordinates. Without `ll`, the pin is placed from `mi` and `ang` (an estimate).
- `CEN` (search for `const CEN`) is the center of the map, the "You" spot.
- `REF` (search for `const REF`) is the state average used in the "Prices near you" box. Update the price and date now and then.

## Things to know

- **The prices are a snapshot, not live.** They were copied from a few web sources on different dates, and some disagree with each other. The app marks those as low confidence. Use the "Save price" box to enter what you actually see.
- **The "Estimate the price now" button only works inside Claude.** On GitHub Pages it stays hidden.
- Station coordinates are estimates until you add `ll`.
- Your typed prices, discounts, car details, radar setting and page color are saved in your browser only (localStorage), not on a server.
- The map tiles come from OpenStreetMap's public tile server, which is fine for a small project. If the app gets a lot of traffic, use a tile provider with its own plan.

## Next step: live prices

To get real live prices you need a gas price data service (an API) and a small server or serverless function to call it, so your API key stays private. Do not put an API key in `index.html`, because anyone can read it. Check each provider's terms and compare a few results against real pump prices before trusting it.

## Credits

Map: [Leaflet](https://leafletjs.com) with [OpenStreetMap](https://www.openstreetmap.org/copyright) tiles (© OpenStreetMap contributors).
