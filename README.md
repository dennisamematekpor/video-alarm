# The Appointed Hour

A minimalist video alarm. Paste a YouTube link, set a time, and it plays full-screen when that hour arrives — like an alarm clock that wakes you with a video instead of a beep.

**Live:** https://dennisamematekpor.github.io/video-alarm/

> Single self-contained `index.html` — no build step, no dependencies, no server. Open it, and it works.

---

## What it does

- Schedule any **YouTube** video to play at a time you choose.
- Three schedule modes:
  - **Every day** — a daily ritual.
  - **Days** — repeat on selected weekdays (e.g., Mon / Wed / Fri).
  - **A date** — fire once on a specific calendar date, then retire itself.
- A full-screen player takes over at the appointed time, with a one-tap link to open the video on YouTube if needed.
- Optional **start muted**, per alarm.
- A live clock, the current date, the time until your next alarm, and a rotating line of maxims.
- Your alarms are saved in the browser — they're there when you come back.

## How to use

1. Open the page.
2. Paste a YouTube link, pick a **Play at** time, and (optionally) add a label.
3. Choose a schedule: **Every day**, specific **Days**, or **A date**.
4. Press **Set the hour**.
5. **Leave the tab open.** When the time comes, the video plays.

Toggle any alarm on/off with its switch, or remove it with ×.

## Add to your home screen

On iPhone/iPad (Safari) or Android (Chrome), use **Share → Add to Home Screen**. It installs with the clock icon and opens full-screen like a native app. (It still only runs while open — see Limitations.)

## Run it locally

Because YouTube requires a valid page origin, opening the file directly with `file://` shows *Error 153*. Serve it over `http://` instead:

```bash
cd path/to/folder
python3 -m http.server 8000
# then open http://localhost:8000/
```

Hosting it (e.g., GitHub Pages) avoids this entirely, since the live site already has a real `https://` origin.

## How it works

- One HTML file: structure, styling, and logic together.
- Alarms persist via the browser's `localStorage`.
- A 1-second loop compares the current local time to each enabled alarm and triggers a match.
- Playback uses the `youtube-nocookie.com` embed with autoplay; a referrer policy is set so modern YouTube embeds load correctly.
- All date logic uses **local** time, so an alarm fires on the day you picked regardless of timezone.

## Limitations

- **The tab must stay open.** A browser tab can't wake itself once closed, so this is not a background alarm. Leave it running (an "Add to Home Screen" instance counts too, while open).
- **Sound on autoplay** depends on the browser. YouTube usually plays with sound once the page has been interacted with; if it's blocked, the embed shows its own play button.
- **Some videos can't be embedded.** If an owner disables embedding, use the **Open on YouTube** link in the player bar.

## Files

```
index.html              the app
manifest.webmanifest    install metadata (name, icon, theme)
icon.svg                scalable favicon
favicon-32.png          fallback favicon
apple-touch-icon.png    iOS home-screen icon (180×180)
icon-192.png            home-screen / manifest icon
icon-512.png            home-screen / manifest icon
```

## License

MIT — use, adapt, and share freely.
