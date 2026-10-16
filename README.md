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
@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@1/base/theme.css");

:root {
    --brand-name: "MyTV";
}
```

Change `MyTV` to whatever you want shown in the top bar. Delete the `:root { ... }` block to keep the default ("JELLYFIN").

Then leave the dashboard and hard-refresh the page (Ctrl+Shift+R, or Cmd+Shift+R on a Mac).

`@1` always loads the newest 1.x release, so you get updates without changing anything.

#### On a TV

The Custom CSS lives on your server, so there's nothing to install on the TV itself:

1. Set up the theme on the server as above (from a computer is easiest).
2. On the TV, install the **Jellyfin** app (LG Content Store on webOS) and sign in to your server.
3. In the TV app, open `Settings > Display` and check that **Display Mode** is **Auto** (or **TV**), and that **Disable server-provided custom CSS code** is **off**. These are per-device, so set them on the TV itself.
4. Fully close the app and open it again to load the theme. On LG, open the running-apps view and swipe the app closed, or restart the TV.

The TV downloads the theme and fonts from the internet. If your TV has no internet access (local network only), paste the full contents of `base/theme.css` (and any seasonal file under it) into the Custom CSS box instead of the `@import` lines.

<hr>

### Seasonal themes

Seasonal themes load on top of the base theme and change colours and decorations. Add the line for the one you want under the base `@import`:

| Season | Line to add |
| --- | --- |
| Halloween | `@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@1/seasonal/halloween/theme.css");` |

Only load one seasonal theme at a time. All `@import` lines must come before the `:root { ... }` block. To go back to the base look, delete the seasonal line.

#### Halloween

A pumpkin-orange look on purple-black, with decorations:

| Decoration | Where | Switch |
| --- | --- | --- |
| Jack-o'-lanterns | Glowing pumpkins in both bottom corners | `--hw-pumpkins` |
| Hanging bats | Bats on threads under the top bar, swinging gently | `--hw-hanging-bats` |
| Flying bats | A small flock that crosses the screen every 30 seconds or so | `--hw-flying-bats` |
| Spider web | Top-right corner, with a dangling spider | `--hw-web` |
| Orange glow | A warm glow along the bottom edge | `--hw-glow` |
| Moon | Full moon on the sign-in page | `--sf-login-art` |
| Logo pumpkin | Small pumpkin next to your brand name | `--season-badge-size` |

All decorations are on by default. To use Halloween with everything on, your Custom CSS looks like this:

```css
@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@1/base/theme.css");
@import url("https://cdn.jsdelivr.net/gh/rambalasb/seasonfin@1/seasonal/halloween/theme.css");

:root {
    --brand-name: "MyTV";
}
```

To turn decorations off, add their switches to the same `:root { ... }` block. Copy only the lines for the ones you want to hide:

```css
:root {
    --brand-name: "MyTV";

    --hw-pumpkins: none;         /* no jack-o'-lanterns */
    --hw-hanging-bats: none;     /* no hanging bats */
    --hw-flying-bats: none;      /* no flying bats */
    --hw-web: none;              /* no spider web */
    --hw-glow: none;             /* no orange glow along the bottom */
    --sf-login-art: none;        /* no moon on the sign-in page */
    --season-badge-size: 0px;    /* no pumpkin next to the logo */
}
```

Decorations never block clicks or the remote, and they hide while a video plays. On phones the pumpkins are smaller and the flying bats are left out. If your device is set to reduce motion, the bats stay still.

#### Making a new seasonal theme

Copy `seasonal/_template/` to `seasonal/<season>/` and fill in the values:

- **Colours:** `--sf-accent`, `--sf-bg` and `--sf-surface` set most of the look. Set each colour's `-rgb` version to the same colour, or some highlights will keep the old colour.
- **Text on buttons:** for a light accent (yellow, pink, orange), set `--sf-on-accent` to a near-black so button text stays readable.
- **Logo icon:** `--season-badge` puts a small icon next to the logo.
- **Sign-in page:** `--sf-login-art` adds extra background layers, such as a moon or snow.
- **Decorations:** see the second half of `seasonal/halloween/theme.css` for how to place them. Give each one a switch with `display: var(--xx-name, block)` (using a short prefix for the season), and list the switches in this README the way Halloween does.

<hr>

### Repo layout

```
base/theme.css         the main theme (always load this first)
seasonal/<season>/     one folder per seasonal theme
seasonal/_template/    starting point for a new season
```

### Releasing

Push changes to `main`, then tag a release (`git tag v1.1.0 && git push origin v1.1.0`). Installs using `@1` pick it up from the CDN, usually within a day. Use a new major version (`v2.0.0`) only for changes that would break people's existing setups.

### Disclaimer

SeasonFin is a fan project. It is not affiliated with or endorsed by Jellyfin or Netflix.

### License

[MIT](LICENSE)
