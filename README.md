# Flexoki for JetBrains

Light and dark [Flexoki](https://stephango.com/flexoki) themes for GoLand / IntelliJ-based
IDEs, with matching editor color schemes. Designed to pair with GoLand's native
**Sync with OS** so it tracks the macOS light/dark appearance (the same way Ghostty does).

This is a **resource-only** plugin (no compiled code), so it builds with just `zip` — no
JDK or Gradle required.

## Layout

```
flexoki-jetbrains/
├── META-INF/
│   ├── plugin.xml              # declares the two themeProviders
│   └── MANIFEST.MF
├── themes/
│   ├── flexoki-light.theme.json   # UI chrome  → references flexoki-light.xml
│   ├── flexoki-light.xml          # editor color scheme (syntax highlighting)
│   ├── flexoki-dark.theme.json
│   └── flexoki-dark.xml
├── flexoki-plugin.zip          # ← install THIS (Flexoki/lib/flexoki.jar)
└── flexoki.jar                 # bare jar (also installable)
```

## Build

```sh
cd ~/flexoki-jetbrains
zip -q -r flexoki.jar META-INF themes
rm -rf dist && mkdir -p dist/Flexoki/lib && cp flexoki.jar dist/Flexoki/lib/
(cd dist && zip -q -r ../flexoki-plugin.zip Flexoki)
```

## Install

1. GoLand → **Settings** (`⌘,`) → **Plugins** → gear icon ⚙ → **Install Plugin from Disk…**
2. Select `~/flexoki-jetbrains/flexoki-plugin.zip`
3. Restart GoLand when prompted.

## Make it adaptive (track macOS appearance)

Settings → **Appearance & Behavior → Appearance**:

- Check **Sync with OS**
- Click **Light/Dark** (or the gear next to it) and map:
  - **Light theme** → `Flexoki Light`
  - **Dark theme** → `Flexoki Dark`

Now GoLand switches both UI chrome and editor colors automatically with the system —
no wrapper script needed (unlike the k9s skin).

## Syntax color mapping

The palette is exact Flexoki (light = 600 weights, dark = 400 weights). Token assignment:

| Token              | Light       | Dark        |
|--------------------|-------------|-------------|
| Keyword            | red `#AF3029`    | `#D14D41` |
| String             | green `#66800B`  | `#879A39` |
| Function           | orange `#BC5215` | `#DA702C` |
| Type / Class       | yellow `#AD8301` | `#D0A215` |
| Number             | purple `#5E409D` | `#8B7EC8` |
| Constant           | cyan `#24837B`   | `#3AA99F` |
| Parameter / Field  | blue `#205EA6`   | `#4385BE` |
| Annotation         | magenta `#A02F6F`| `#CE5D97` |
| Comment            | base-600 `#6F6E69` | base-500 `#878580` |

The terminal/run-console ANSI palette is mapped to match **Ghostty Flexoki** exactly.

## Notes

- The **editor color scheme** (`*.xml`) is the high-fidelity part. The **UI chrome**
  (`*.theme.json`) is a conservative Flexoki tint over the base IntelliJ Light/Darcula
  theme and may want in-IDE tweaks (Settings → Appearance, and the theme JSON `ui` block).
- To iterate on the editor colors live without rebuilding: Settings → Editor → Color Scheme,
  duplicate, and tweak; or re-run the build and reinstall.
- Palette by Steph Ango (MIT). This port: Haoxin Yang.
```
