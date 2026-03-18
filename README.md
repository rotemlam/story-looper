# 🌙 Story Looper / עוד פעם

A minimal web app for repeating podcast episodes — built for bedtime stories.  
Search for any podcast, paste a Spotify link, save favorites, and loop episodes a set number of times or forever.

**Live demo:** [rotemlam.github.io/repeat.html](https://rotemlam.github.io/repeat.html)

---

## What it does

- Search Spotify for any podcast episode
- Paste a direct Spotify episode link
- Save up to 3 favorite episodes (persisted in your browser)
- Loop an episode N times or indefinitely
- Floating player that stays visible while you browse
- Works on mobile (Android Chrome, iOS Safari)

> **Requires Spotify Premium** — the Web Playback SDK only works with Premium accounts.

---

## Make it yours — step by step

### Step 1 — Create a Spotify Developer App

1. Go to [developer.spotify.com/dashboard](https://developer.spotify.com/dashboard) and log in
2. Click **Create app**
3. Fill in any name and description (e.g. "My Story Looper")
4. Under **Redirect URIs**, add the URL where you'll host the app  
   (e.g. `https://yourusername.github.io/repeat.html`)
5. Click **Save**
6. Copy your **Client ID** from the app dashboard

### Step 2 — Edit `repeat-template.html`

Open the file in any text editor and find this line near the bottom:

```js
const HARDCODED_ID = ''; // ← paste your Spotify Client ID here
```

Paste your Client ID between the quotes:

```js
const HARDCODED_ID = 'abc123youridhere456';
```

**Optional:** if you want a collaborative playlist button (to save episodes to a shared playlist), find:

```js
const COLLAB_PLAYLIST_ID = ''; // ← paste your collaborative playlist ID here
```

Paste your Spotify playlist ID (the string of letters/numbers in the playlist URL).

**Optional:** to pre-save a default favorite episode, find:

```js
const DEFAULT_FAVORITES = [
  null,
  null,
  null
];
```

Replace the first `null` with an episode object:

```js
const DEFAULT_FAVORITES = [
  {
    uri: 'spotify:episode:YOUR_EPISODE_ID',
    name: null,   // fetched automatically after login
    show: null,
    image: null,
    startMs: 0    // start position in milliseconds (0 = from beginning)
  },
  null,
  null
];
```

To find an episode ID: open the episode in Spotify, click **Share → Copy Episode Link**.  
The ID is the string after `/episode/` in the URL.

### Step 3 — Rename the file (optional)

Rename `repeat-template.html` to whatever you like — `index.html`, `stories.html`, etc.  
Just make sure the filename matches the Redirect URI you set in Step 1.

### Step 4 — Upload to GitHub Pages

1. Create a new GitHub repository at [github.com/new](https://github.com/new)
2. Name it `<yourusername>.github.io` (for a personal site) or any name (for a project site)
3. Upload your edited HTML file and this README
4. Go to **Settings → Pages** → set Source to **Deploy from a branch → main → / (root)**
5. Your app will be live at `https://yourusername.github.io/repeat.html` within a minute

> **Important:** the URL in GitHub Pages must exactly match the Redirect URI you set in your Spotify app. If they don't match, login will fail with a redirect_uri_mismatch error.

---

## Sharing with others

By default, Spotify apps are in **Development Mode** — only users you explicitly add in the dashboard can log in (up to 25 people).

To allow anyone to use your app:
1. Go to your app in the Spotify dashboard
2. Click **Settings → Request Extended Quota Access**
3. Describe your use case briefly and submit
4. Spotify usually approves within a few days

Until then, add friends manually: **Dashboard → Users and Access → Add new user** (requires their Spotify email address).

---

## Customizing the look

The app uses CSS variables at the top of the `<style>` block. The main ones to change:

```css
--pink:      #d4849a;   /* accent color — buttons, hearts, progress */
--gold:      #c9a96e;   /* secondary accent — labels, timestamps */
--navy:      #0d1b2a;   /* background */
--cream:     #f5ede8;   /* primary text */
```

The Hebrew text can be changed to any language — search for Hebrew strings in the HTML and JS sections.

---

## Technical notes

- **Single HTML file** — no build step, no dependencies, no server needed
- **Spotify Web Playback SDK** — loaded from Spotify's CDN, controls playback directly in the browser
- **PKCE OAuth** — secure login flow that works without a backend server
- **localStorage** — favorites and login state are stored in the browser, never sent anywhere
- Tested on: Chrome (Android + Desktop), Safari (iOS + macOS), Firefox (Desktop)

---

## License

MIT — do whatever you want with it. Credit appreciated but not required.
