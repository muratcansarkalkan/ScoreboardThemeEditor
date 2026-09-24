# NBA Live Scoreboard Theme Editor

NBA Live Scoreboard Theme Editor is a visual editor for custom scoreboard themes used by the NBA Live ASI plugin.

For a complete first-time-user walkthrough covering the scoreboard, stat/player-foul popups, violations, play calls, intro, starting lineups, outro, in-game lineups, bindings, assets, fonts, and live reload, see **[USER_GUIDE.md](USER_GUIDE.md)**.

Open a theme such as:

```text
assets\popups\TEST\scoreboard\scoreboard.json
```

Select preview teams and drag scoreboard elements directly on the canvas. The editor supports exact bounds, behavior rules, font settings, simulated game data, and asset-backed team previews.

## Features

The editor supports:

- Draggable scoreboard elements with precise position and size controls
- Ordered layers with duplication, deletion, locking, visibility, and Z-order controls
- Rectangle, image, text, and indicator elements
- Fixed colors and team-color bindings
- Solid fills and two-color horizontal or vertical gradients
- Text alignment, capitalization, small caps, overflow, fit, and fitWidth (horizontal condense) modes
- Text templates containing multiple live values
- Text stroke and shadow effects
- Color pickers for text, tint, fills, gradients, scoreboard backgrounds, and shot-clock colors
- Preview backgrounds for 4:3, 16:9, and 16:10 displays

The preview uses the same centered placement, reference resolution, offsets, and uniform or fixed scaling rules as the in-game renderer.

## Theme structure

Custom themes are stored under:

```text
assets\popups\<theme-name>\
```

The main scoreboard layout is stored at:

```text
assets\popups\<theme-name>\scoreboard\scoreboard.json
```

Images, fonts, team logos, and other theme assets should remain inside the corresponding theme directory.

The editor automatically migrates legacy named scoreboard properties into an ordered `elements[]` collection.

## Layers

The **Layers** tab can:

- Add rectangles, images, text, and indicators
- Duplicate or delete layers
- Change layer order
- Hide or lock layers
- Select hidden or locked layers from the layer list

The **Element** tab controls:

- Position and dimensions
- Opacity and visibility
- Locking
- Horizontal and vertical alignment
- `overflow`, `fit`, and `fitWidth` behavior
- Solid fills
- Horizontal and vertical gradients
- Image tinting
- Text stroke and shadow settings

Primary and secondary team-color panels are ordinary layers and can be edited like any other element.

## Fonts and text

The **Font** tab independently controls the appearance of:

- Team scores
- Game clock
- Shot clock
- Team names
- Period
- Numeric and text fouls
- Numeric and text timeouts
- BONUS indicators

Dot, bar, and image indicator sizes are controlled through their draggable element bounds.

### Text templates

A text element can combine static text with multiple live values:

```json
"template": "{away.name} {away.score} - {home.score} {home.name}"
```

Another example:

```json
"template": "TIMEOUTS: {home.timeouts}"
```

Use doubled braces to display literal braces:

```json
"template": "{{LIVE}} {game.clock}"
```

### Stroke and shadow

Text elements support an optional stroke and hard-edged shadow:

```json
{
  "type": "text",
  "template": "TIMEOUTS: {home.timeouts}",
  "textColor": 16777215,
  "stroke": {
    "enabled": true,
    "color": 0,
    "width": 2
  },
  "shadow": {
    "enabled": true,
    "color": 0,
    "alpha": 180,
    "offsetX": 2,
    "offsetY": 2
  }
}
```

Text is rendered in this order:

1. Shadow
2. Stroke
3. Main text

## Available bindings

Useful scoreboard bindings include:

```text
away.primaryColor       home.primaryColor
away.secondaryColor     home.secondaryColor
away.logo                home.logo
away.name                home.name
away.score               home.score
away.fouls               home.fouls
away.timeouts            home.timeouts
away.bonus               home.bonus
game.clock               game.shotClock
game.period
```

Use `type: "indicator"` for foul or timeout bindings.

Gradient endpoints can use either a fixed decimal RGB color or one of the four team-color bindings.

## End-user installation

Keep these four files together in the same directory:

```text
NBALiveScoreboardEditor.exe
NBALiveScoreboardEditor.dll
NBALiveScoreboardEditor.deps.json
NBALiveScoreboardEditor.runtimeconfig.json
```

`NBALiveScoreboardEditor.pdb` contains debugging symbols and is not required by end users.

### Requirements

The framework-dependent release requires:

- Windows
- Microsoft .NET 8 Desktop Runtime
- The release files listed above

The ordinary .NET Runtime is not sufficient because the editor uses WPF. Install the **.NET 8 Desktop Runtime** matching the application architecture.

The .NET SDK and Visual Studio are only required when building the editor from source.

## Build from source

Open `ScoreboardThemeEditor.csproj` in Visual Studio 2022 with the .NET 8 SDK installed, or run:

```powershell
dotnet build -c Release
```

The compiled files will be placed under the project's `bin\Release` directory.

## Live workflow

1. Run NBA Live with the updated ASI plugin.
2. Pause the game.
3. Open and edit the active theme.
4. Click **Save + Reload in Game**.
5. Resume the game.

The editor updates the theme's `.reload` marker. The plugin checks this marker every 500 milliseconds from the Direct3D 9 render thread.

`F5` remains available as a manual reload method.

The current editor can switch among the main scoreboard, Stats, Intro, Violation, Playcall, Starting Lineup, Outro, and In-Game Lineups when the corresponding layout files exist in the popup package.
### Player jersey numbers in stat / foul popups

Player stat layouts can display the featured player's jersey number with a normal text element using `player.jerseyNumber`. The editor includes a **Jersey #** layer button that creates this binding automatically, plus a **Jersey #** preview value in Preview Data. Example:

```json
{
  "id": "playerJerseyNumber",
  "type": "text",
  "binding": "player.jerseyNumber"
}
```
