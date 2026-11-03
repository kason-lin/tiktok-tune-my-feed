# TikTok · Tune My Feed (demo prototype)

A clickable TikTok-style app (plain HTML/CSS/JS, no build step) that adds one new feature: **Tune My Feed**. Long-press any video, tap *Tune My Feed*, set how much of each topic you want, and the upcoming For You videos are re-ranked right away.

This is a concept prototype for a demo. It is not affiliated with TikTok. 

## Why this exists

**The problem.** I interviewed 7 college students about how they use TikTok. The top frustration: when the For You feed goes off (one friend-sent video can skew it), there's no fast way to fix it, so people switch to Instagram Reels. TikTok does have topic settings, but they're buried in Settings.

**The idea.** Put feed control where users already are. Long-press a video, right where "Not interested" lives, and turn each topic up, down or off. The next videos change immediately instead of after days of retraining.

**What to try.** Open the live demo, long-press any video, tap *Tune My Feed*, drag Food to "More" and save. Upcoming videos re-rank on the spot. In a demo run, that took Food from about 1 in 10 upcoming videos to 5 in 10.

**What happened.** 3 of 3 NYU students in a usability test found the long-press menu and used the sliders without help. I pitched the MVP to 7 product managers at the NYU Product Management Club.

**How it was built.** Plain HTML, CSS and JavaScript, built with Claude Code. Each slider sets a topic's weight, and the queue re-ranks 45 videos across 6 topics.

Full case study: https://www.kasonlin.com/tiktok.html

## Try it live

**👉 https://tiktok-tune-my-feed.vercel.app**

Works on any phone or laptop, no setup needed. On a laptop it shows inside an iPhone frame.

**On an iPhone:** open the link in Safari, tap Share → **Add to Home Screen**, then open it from the home screen. It runs full-screen with no Safari bars, like a real app.

## Updating the live site

The site is hosted on Vercel and connected to this GitHub repo. Every push to `main` redeploys it automatically in about 30 seconds:

```bash
git add .
git commit -m "What I changed"
git push
```

## Run it locally (optional)

For offline work or testing changes before pushing, run this from this folder:

```bash
python3 -m http.server 8000 --bind 0.0.0.0
```

Then open http://localhost:8000. To try it on a phone on the same Wi-Fi, find your laptop's IP with `ipconfig getifaddr en0` and open `http://<that-ip>:8000`. If macOS asks whether Python can accept incoming connections, click **Allow**.

## Files

| File | What it is |
|---|---|
| `index.html` | App shell (feed, top bar, bottom nav, phone frame) |
| `styles.css` | All visuals |
| `app.js` | Feed, gestures, sheets, screens, ranking engine, demo panel |
| `icons.js` | Inline SVG icons |
| `data/videos.json` | The 45 videos (topic, creator, caption, sound, counts) |
| `data/videos.js` | Copy of the JSON, used only if you open `index.html` directly without the server |
| `videos/` | 720×1280 H.264 clips with music (≈3 MB each) plus a `.jpg` poster for each |
| `img/avatars/` | Creator avatars (cropped from the clips) |
| `DEMO.md` | 60-second walkthrough script |

**To swap in your own clips:** drop a vertical `.mp4` and a `.jpg` poster into `videos/`, then add or edit an entry in `data/videos.json`. `topic` must be one of `food, travel, music, fitness, pets, comedy`. If you edit the JSON, regenerate the fallback with:

```bash
python3 -c "import json;d=json.load(open('data/videos.json'));open('data/videos.js','w').write('window.VIDEOS_FALLBACK = '+json.dumps(d,ensure_ascii=False)+';\n')"
```

## Demo controls
- **Demo panel:** press `D` (laptop), tap the video with two fingers (phone), or triple-tap the status bar. It shows the topic mix of the next 10 videos before and after your last save, and has a **Reset demo** button.
- **Laptop keys:** ↑/↓ or the scroll wheel = swipe, Space = pause, L = like, M = mute, H = long-press menu, Esc = back.

## Credits
Video clips and music are from [Mixkit](https://mixkit.co) under the free Mixkit license. Track names are shown as each video's sound. Font: TikTok Sans (Google Fonts).
