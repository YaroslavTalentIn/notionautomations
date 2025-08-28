# TalentIn Olympics Timer — PWA kit

Upload these files to your GitHub Pages project (repo root):
- `manifest.json`
- `sw.js`
- `icons/icon-192.png`
- `icons/icon-512.png`
- (Optional for iOS Home Screen) `icons/icon-180.png` + `<link rel="apple-touch-icon" href="icons/icon-180.png">`

### Add these to your existing HTML `<head>`:

```html
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#0f1221">
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icons/icon-180.png">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```

### Register the service worker (before `</body>`):

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./sw.js');
  }
  // Try to keep screen awake during play
  if ('wakeLock' in navigator) {
    let lock; const request = async () => { try { lock = await navigator.wakeLock.request('screen'); } catch {} };
    document.addEventListener('visibilitychange', () => { if (document.visibilityState === 'visible') request(); });
    request();
  }
</script>
```

### iPad full-screen tips
- After adding to Home Screen, the app opens in **standalone** (no Safari UI).
- The bottom **Home bar** cannot be fully hidden by web apps, but it fades during inactivity.
- To prevent sleep during the game: **Settings → Display & Brightness → Auto-Lock → Never** (or use **Guided Access**).

