# Grammarly Desktop App

An Electron wrapper for Grammarly web app that provides a clean, dedicated application experience.

## Features

- Runs Grammarly in a dedicated window without browser controls
- Clean interface focused just on writing and editing
- System tray integration
- Desktop notifications for Grammarly alerts

## Installation

### Prerequisites
- Node.js (v14+)
- npm (v6+)
- Git

### Method 1: Build from Source

1. Clone this repository:
```bash
git clone git@github.com:YOUR_USERNAME/grammarly-electron.git
cd grammarly-electron
```

2. Install dependencies:
```bash
npm install
```

3. Run the app:
```bash
npm start
```

### Method 2: Install Pre-built Package

#### AppImage (Recommended)
1. Download the latest AppImage from the releases page
2. Make it executable:
```bash
chmod +x Grammarly-*.AppImage
```
3. Extract it (necessary due to sandbox permissions):
```bash
./Grammarly-*.AppImage --appimage-extract
```
4. Create a desktop shortcut:
```bash
cat > ~/.local/share/applications/grammarly-app.desktop << EOF
[Desktop Entry]
Name=Grammarly
Comment=Grammarly Desktop App
Exec=$(realpath /path/to/squashfs-root/zyzd-grammarly) --no-sandbox
Terminal=false
Type=Application
Categories=Office;TextTools;
Icon=$(realpath /path/to/build/icons/256x256.png)
StartupWMClass=zyzd-grammarly
EOF
```
5. Update desktop database:
```bash
update-desktop-database ~/.local/share/applications
```

#### Debian Package
```bash
sudo dpkg -i grammarly_*.deb
sudo apt-get -f install  # To resolve any dependencies
```

## Building from Source

To build the app into distributable formats:

```bash
# Install development dependencies
npm install --save-dev electron-builder

# Build for Linux
npm run build
```

This will create AppImage and .deb packages in the `dist` directory.

### Building with Custom Icons

If you want to use custom icons:

1. Place your icons in the `build/icons` directory with the following sizes:
   - 16x16.png
   - 32x32.png
   - 64x64.png
   - 128x128.png
   - 256x256.png
   - 512x512.png

2. Update the package.json "build" section if needed:
```json
"build": {
  "appId": "com.your-name.grammarly",
  "productName": "Grammarly",
  "linux": {
    "target": ["AppImage", "deb"],
    "category": "Office",
    "icon": "build/icons",
    "maintainer": "Your Name <your.email@example.com>"
  }
}
```

## Troubleshooting

### Sandbox Issues
If you encounter sandbox-related errors, run the application with the `--no-sandbox` flag:
```bash
./Grammarly-*.AppImage --no-sandbox
```

### AppImage Extraction
If FUSE is not available on your system, you can extract the AppImage:
```bash
./Grammarly-*.AppImage --appimage-extract
./squashfs-root/zyzd-grammarly --no-sandbox
```

### Missing Libraries
For issues with missing libraries, install the standard development packages:
```bash
sudo apt-get install libgtk-3-0 libnotify4 libnss3 libxss1 libxtst6 xdg-utils libatspi2.0-0 libdrm2 libgbm1 libxcb-dri3-0
```

## License

MIT
