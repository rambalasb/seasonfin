# SeasonFin

A dark, streaming-style theme for Jellyfin's web client, with seasonal looks you can switch on for Halloween, Diwali, Christmas, New Year, Valentine's Day, spring, summer and more. Put your own name in the logo with one line.

<hr>

### Requirements

- **Jellyfin 12.x**
- **Display Mode set to Auto** (`User Settings > Display > Display Mode > Auto`). Computers get the full-width layout, phones get the mobile layout, and TVs get the TV layout. All three are styled.

#### TVs

SeasonFin works in the LG webOS Jellyfin app, and in other TV apps that use Jellyfin's web client, because they load the same Custom CSS from your server. It supports **webOS 5 (2020 TVs) and newer**. On TVs it uses lighter effects (no blur), and everything you can select with the remote gets a clear white or accent highlight.

<hr>

### How to install

In Jellyfin, go to `Dashboard > Branding`, paste this into the **Custom CSS code** box and click **Save**:

```css
@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@main/base/theme.css");

:root {
    --brand-name: "MyTV";
}
```

Change `MyTV` to whatever you want shown in the top bar. Delete the `:root { ... }` block to keep the default ("JELLYFIN").

Then leave the dashboard and hard-refresh the page (Ctrl+Shift+R, or Cmd+Shift+R on a Mac). On a TV, close and reopen the Jellyfin app.

<hr>

### Seasonal themes

Seasonal themes load on top of the base theme and change colours and decorations. Add the line for the one you want under the base `@import`:

| Season | Line to add |
| --- | --- |
| Halloween | `@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@main/seasonal/halloween/theme.css");` |

Only load one seasonal theme at a time. All `@import` lines must come before the `:root { ... }` block. To go back to the base look, delete the seasonal line.

#### Making a new seasonal theme

Copy `seasonal/_template/` to `seasonal/<season>/` and fill in the values:

- **Colours:** `--sf-accent`, `--sf-bg` and `--sf-surface` set most of the look. Set each colour's `-rgb` version to the same colour, or some highlights will keep the old colour.
- **Text on buttons:** for a light accent (yellow, pink, orange), set `--sf-on-accent` to a near-black so button text stays readable.
- **Logo icon:** `--season-badge` puts a small icon next to the logo.
- **Sign-in page:** `--sf-login-art` adds extra background layers, such as a moon or snow.

<hr>

### Repo layout

```
base/theme.css         the main theme (always load this first)
seasonal/<season>/     one folder per seasonal theme
seasonal/_template/    starting point for a new season
```

### Disclaimer

SeasonFin is a fan project. It is not affiliated with or endorsed by Jellyfin or Netflix.

### License

[MIT](LICENSE)
