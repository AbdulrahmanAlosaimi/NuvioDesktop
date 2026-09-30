<div align="center">

  <img src="https://nuvio.tv/assets/nuvio-app-logo-wordmark.webp" alt="Nuvio" width="320" />

  <p>
    A free, open-source media app for Windows, macOS, and Linux.
    <br />
    Bring your own sources. Nuvio turns them into a library with artwork, ratings, subtitles, and your place saved on every screen.
  </p>

  [Website](https://nuvio.tv) · [GitHub releases](https://github.com/NuvioMedia/NuvioDesktop/releases/latest) · [Support Nuvio](https://nuvio.tv/support)

</div>

## ⚠️ Alpha Software - Slow Development - Testers Only

Nuvio Desktop is currently in alpha and is intended only for testers. It is under development and is not suitable for daily use.

Expect breaking changes with every update. Features, settings, stored data, and compatibility may change or stop working without notice. Do not rely on this build as your primary media app, and report any issues you encounter during testing.

## Get Nuvio Desktop

Download the latest build from [GitHub Releases](https://github.com/NuvioMedia/NuvioDesktop/releases/latest).

- Windows: MSI installer
- macOS: DMG installer
- Linux: DEB, RPM, Flatpak, or AppImage

## Build from source

```bash
git clone https://github.com/NuvioMedia/NuvioDesktop.git
cd NuvioDesktop
```

### Run the app

```bash
./gradlew :composeApp:run
```

On Windows PowerShell:

```powershell
.\gradlew.bat :composeApp:run
```

### Package the app

Build a release package for the current host:

```bash
./gradlew :composeApp:packageReleaseDistributionForCurrentOS
```

For platform-specific packaging:

Windows PowerShell:

```powershell
.\gradlew.bat :composeApp:packageReleaseMsi --rerun-tasks
```

macOS:

```bash
./scripts/build-macos-release-dmgs.sh --package-only
```

Linux:

```bash
./gradlew :composeApp:packageReleaseDeb
```

The shared app is built with Kotlin Multiplatform and Compose Multiplatform.

### Advanced: custom mpv configuration (Windows)

The Windows player bridge accepts two environment variables, both read when playback starts and
therefore requiring a full restart of Nuvio:

| Variable | Effect |
| --- | --- |
| `NUVIO_LIBMPV_PATH` | Load a replacement `libmpv-2.dll` instead of the bundled copy. |
| `NUVIO_MPV_CONFIG_DIR` | Load `mpv.conf`, `input.conf`, `scripts/` and `shaders/` from an mpv configuration directory. Unset by default, which keeps config loading disabled exactly as before. |

This is an unsupported, opt-in power-user escape hatch — it exists to unlock native filter chains,
custom shaders and custom `libmpv` builds. There is no settings UI, and options named in your
`mpv.conf` override Nuvio's own playback defaults.

See [`composeApp/src/desktopMain/native/windows/README.md`](composeApp/src/desktopMain/native/windows/README.md)
for the full reference: precedence rules, known conflicts, current limitations, and how to rebuild
just `player_bridge.dll` — including a hosted GitHub Actions workflow for contributors without a
local Windows toolchain.

## License

[GNU General Public License v3.0](./LICENSE)
