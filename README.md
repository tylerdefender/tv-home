# tv-home

A simple, fast home screen for a Samsung Tizen TV (built for the QN900A, Tizen 6.0).

- `index.html` – the launcher (clock + app tiles). Works in the TV browser (cursor) and as an installed Tizen app (remote arrows + native app launch).
- `config.xml`, `icon.png` – Tizen web app packaging.

## Quick use (no computer): TV browser
Publish with GitHub Pages and set the page as the TV browser homepage. Tiles open websites only; most streaming sites will not play video here (DRM).

## Install as a real Tizen app (needs a Windows/Mac/Linux computer, ~30 min)
Installed apps can launch the native Netflix/YouTube/etc. apps.

### 1. Enable Developer Mode on the TV
1. TV home → **Apps** panel.
2. On the remote, type **1 2 3 4 5**.
3. Turn Developer mode **On**, enter the computer's local IP address, then **restart the TV**.

### 2. Set up the computer
1. Install **Tizen Studio** with the **TV Extensions** package (Package Manager → Extension SDK → TV Extensions).
2. Make sure the computer and TV are on the same Wi‑Fi/network.
3. Tizen Studio → **Tools → Device Manager → Remote Device Manager → +**, enter the TV's IP address (port 26101), switch the connection on.
4. **Tools → Certificate Manager → +**: create a **Samsung** certificate (log in with a Samsung account; select the TV as the target device) .

### 3. Build and run
1. **File → New → Tizen Project → Template → TV → Web Application → Basic**, then replace its files with `index.html`, `config.xml`, `icon.png` from this repo (or import this folder as an existing project).
2. Right-click the project → **Run As → Tizen Web Application**. The app installs on the TV and launches.

Re-install if the certificate expires or Developer Mode resets.

### Native app IDs
`index.html` has an `appIds` map. IDs vary by TV model and region, and the ones included are unverified. To find the real ones on your TV, with the TV connected over `sdb`:

    sdb shell 0 applist

Copy the IDs for Netflix, YouTube, etc. into `appIds` in `index.html` (keys: `netflix`, `prime`, `youtube`, `hbo`, `disney`, `hulu`, `peacock`). Tiles without an ID fall back to opening the website.
