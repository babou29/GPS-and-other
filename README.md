
# 📸 Photobooth Enhancements – GPS, Stability & Admin Tools

Author: TchatGpt->**Babou29**
---
Hello,
Here are some ideas I had, but I got help from ChatGpt because I don't have programming knowledge.

I wanted to suggest these ideas for inclusion in future versions.

Thank you.
Sincerely,
Babou29
---

This package documents enhancements made to the open‑source Photobooth project to improve:

- 📍 GPS tagging of photos
- 📷 EXIF metadata automation
- 🔢 Camera shutter counter
- 🖥 Mobile admin interface
- 🛠 Camera watchdog (anti‑freeze)
- 🌐 Local HTTPS access
- ⚡ Performance improvements (RAM preview)

These features are designed for **event photobooths** running on Debian/Linux with DSLR cameras (e.g. Nikon D3300).

---

# 🚀 Features

## GPS tagging from smartphone
Guests or operators can send their GPS location from a smartphone.  
The system automatically embeds coordinates into photo EXIF metadata.

## Automatic EXIF metadata
Each photo receives:

- GPS coordinates
- Creator name
- Software name
- Event name


## Mobile Admin Interface

File:

web/admin2.html

Features:

- send GPS coordinates
- display camera shutter count
- display photo counter
- display disk usage

Deployment location:

/var/www/html/admin2.html

## Camera watchdog
A background service monitors the camera and resets USB if the device freezes.

## Mobile admin panel
A lightweight page allows:

- sending GPS position
- reading camera shutter count
- counting photos taken
- checking disk usage

## Local HTTPS
Secure connection via:

```
https://photobooth.local
```

Works without internet using **mDNS (Avahi)**.

---

# 📂 Repository structure

```
docs/
scripts/
systemd/
apache/
api_examples/
screenshots/
```

---

# 📊 System architecture

```mermaid
flowchart TD

Camera[Nikon DSLR]
USB --> Gphoto[gphoto2 / cameracontrol.py]

Gphoto --> Photobooth[Photobooth Software]
Photobooth --> Images[/data/images]

Images --> GPSWatcher[gps_watcher.sh]
GPSWatcher --> EXIF[EXIF Metadata]

Smartphone --> AdminPage[admin2.html]
AdminPage --> SaveGPS[save_gps.php]
SaveGPS --> gps.txt

Images --> ShutterAPI[shutter.php]
Images --> PhotoCount[photo_count.php]

Watchdog[camera_watchdog.sh] --> USB
```

---

# ⚙️ Requirements

Debian 12 or compatible.

Required packages:

```
exiftool
inotify-tools
avahi-daemon
usbutils
apache2
php
```

---

# 📜 License

MIT License (recommended for integration into open source projects).

See LICENSE file.

---

# 🤝 Pull Request

If integrating upstream:

1. Add scripts and documentation
2. Integrate optional GPS module
3. Add admin interface extension

A ready PR template is included.

