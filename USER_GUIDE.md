# NBA Live Scoreboard Theme Editor — Complete User Guide

This guide is intended for someone opening the NBA Live Scoreboard Theme Editor for the first time.

The editor creates and edits JSON layouts used by the NBA Live ASI plugin for custom broadcast graphics. A single popup package can contain a scoreboard plus stat graphics, fouls, violations, play calls, introductions, starting lineups, outros, and in-game lineup graphics.

The editor is visual: select an overlay, add or select layers, move and resize them on the preview, assign live-game bindings, and save the JSON. You normally do not need to edit JSON by hand.

---

## 1. Before you begin

You need:

- NBA Live 2005–08 with the current NBA Live ASI Loader / NBA Live Launcher setup.
- A popup theme folder inside `assets\popups\`.
- NBA Live Scoreboard Theme Editor.
- Microsoft .NET 8 Desktop Runtime.

Keep the editor release files together in the same folder.

A popup package typically looks like this:

```text
assets\popups\MYTHEME\
    scoreboard\
        scoreboard.json
        popup.json
        teams.json
        teams\
        images\
        fonts\

    stats\
        player.json
        player_1.json
        player_2.json
        player_3.json
        player_4.json
        player_5.json
        player_foul.json
        team.json
        team_1.json
        team_2.json
        team_3.json
        popup.json
        images\
        fonts\

    violation\
        violation.json

    playcall\
        playcall.json

    intro\
        intro.json

    starting5\
        starting5.json
        portraits\

    outro\
        outro.json

    lineups\
        lineups.json
```

Not every theme must use every folder. Start from an existing working theme and replace or redesign only the layouts you need.

---

## 2. Opening a theme

Click **Open** and select one of the layout JSON files. For a new user, the best starting point is:

```text
assets\popups\MYTHEME\scoreboard\scoreboard.json
```

Once one layout is loaded, use the **Screen** selector at the top of the editor to move between the other supported parts of the same popup package:

- Scoreboard
- Stats
- Intro
- Violation
- Playcall
- Starting Lineup
- Outro
- In-Game Lineups

The editor locates the corresponding sibling folder automatically.

If a layout does not exist, the status bar reports which JSON file it expected.

---

## 3. The editor window

The left/center area is the visual preview. The right-side tabs contain the controls used to build the layout.

### Preview Data

Preview Data supplies fake game information so that live bindings are visible while editing. Changing these values does not edit the game; it changes only the editor preview.

Examples include:

- Away/home score
- Game clock
- Shot clock
- Quarter
- Fouls
- Timeouts
- Violation title and possession text
- Play-call team and play name
- Stat payload values
- Jersey number
- Intro payload values
- Starting-lineup payload values
- Outro payload values
- In-game lineup payload values

Use these fields to test long names, large numbers, different teams, and edge cases before testing in NBA Live.

### Layout tab

The **Layout** tab controls the coordinate system and overall placement of the overlay.

Important fields:

- **Reference width / Reference height** — the resolution against which element coordinates are authored.
- **Scale mode** — determines how the layout is scaled to the actual game resolution.
- **Scoreboard X/Y offset** — moves the entire layout.
- **Scoreboard width/height** — overall layout bounds.
- **Overlay Z-order** — controls which popup appears above another when multiple overlays are active.

You can also load an **Editor reference background**. This is useful for designing over a screenshot of the game. The reference image is editor-only and is not automatically displayed in NBA Live.

Click **Apply Layout** after editing layout values.

### Element tab

The **Element** tab edits the currently selected layer.

It contains:

- Element type
- Data binding
- Static text
- Text template
- Font preset
- Image path
- Image fit
- Tint
- Opacity
- Exact X/Y position
- Width/height
- Z-order
- Visibility
- Editor locking
- Text alignment
- Overflow / fit
- Text transform
- Small caps
- Font height
- Text color
- Stroke
- Shadow
- Fill and gradients

For rough positioning, drag the element directly in the preview. For precise work, type values into X, Y, Width, and Height and click **Apply Element Bounds**.

### Layers tab

The **Layers** tab is the object list for the current layout.

You can:

- Select a layer
- Move it up or down
- Duplicate it
- Delete it
- Add a rectangle
- Add an image
- Add text
- Add a pre-bound **Jersey #** text layer

Hidden and locked elements can still be selected from the Layers list.

### Behavior tab

The **Behavior** tab contains scoreboard-wide display and animation rules.

Depending on the layout, useful options include:

- Background color and alpha
- Background image
- Accent strips
- Scoreboard visibility timing
- Shot-clock visibility threshold
- Urgent shot-clock threshold/color
- Team-name visibility
- Team-logo visibility
- Team-name format
- Period format
- Foul display style
- Timeout display style
- BONUS behavior
- Enter animation
- Hold duration
- Exit animation
- Pause behavior

Click **Preview Animation** to test enter/hold/exit behavior inside the editor.

### Font tab

The **Font** tab controls the default popup font settings.

The main font can define:

- Font file
- Internal font family name
- Weight
- Character spacing
- Score height
- Clock height
- Shot-clock height
- Team-name height
- Period height
- Foul height
- Timeout height
- BONUS height

Layouts can also use named font presets from `popup.json`. An element's **Font preset** field selects one of those presets.

---

# 4. Understanding layers

Each visible object is a layer. Most layouts are constructed from only three practical layer types.

## Rectangle

Use rectangles for:

- Background panels
- Bars
- Team-color strips
- Separators
- Boxes behind text

A rectangle can have:

- Fixed solid color
- Team-color binding
- Horizontal gradient
- Vertical gradient
- Transparency

## Image

Use image layers for:

- Team logos
- Player portraits
- Decorative artwork
- Network-style backgrounds
- Icons

The image can be specified directly with **Image path** or supplied at runtime by a binding such as `away.logo` or `player.portrait`.

Common image-fit modes are **contain** and **stretch**.

## Text

Use text layers for:

- Scores
- Clocks
- Team names
- Player names
- Jersey numbers
- Stat labels and values
- Arena/location text
- Any fixed caption

A text layer can use either static text, a single binding, or a text template.

---

# 5. Live bindings

A **binding** tells the ASI plugin what live value should be shown in an element.

For example:

```text
away.score
```

means "show the away team's current score."

A text element bound to `game.clock` displays the live game clock. An image bound to `home.logo` displays the current home-team logo.

The editor also resolves these bindings in the preview using the values in Preview Data.

---

# 6. Creating the main scoreboard

Select **Screen → Scoreboard**.

The main scoreboard is normally stored at:

```text
scoreboard\scoreboard.json
```

A useful scoreboard commonly contains:

- Background panels
- Away logo
- Home logo
- Away team name
- Home team name
- Away score
- Home score
- Game clock
- Shot clock
- Period
- Fouls
- Timeouts
- BONUS indicators

## Common scoreboard bindings

```text
away.logo
home.logo
away.name
home.name
away.score
home.score
away.fouls
home.fouls
away.timeouts
home.timeouts
away.bonus
home.bonus
game.clock
game.shotClock
game.period
```

Team colors can be used on rectangle fills, gradients, and image tints:

```text
away.primaryColor
away.secondaryColor
home.primaryColor
home.secondaryColor
```

## Basic scoreboard workflow

1. Open `scoreboard.json`.
2. Set the reference resolution in **Layout**.
3. Add background rectangles or images.
4. Add team logos with image bindings.
5. Add team names and scores with text bindings.
6. Add game clock, shot clock, and period.
7. Add foul/timeout indicators if desired.
8. Configure fonts.
9. Configure scoreboard behavior and animation.
10. Save and test in game.

## Team-name formatting

The scoreboard behavior supports different team-name representations. Depending on the selected format, the renderer can use information such as city, nickname, short code, or full team name.

Preview different teams using the Away and Home team selectors.

## Period formatting

The editor supports different period formats, including quarter-style text and numeric forms. Test regulation and overtime presentation before release.

---

# 7. Text templates

A text element does not have to contain only one live value. Use **Text template** to combine static text and bindings.

Example:

```text
{away.name} {away.score} - {home.score} {home.name}
```

Another example:

```text
TIMEOUTS: {home.timeouts}
```

Literal braces use doubled braces:

```text
{{LIVE}} {game.clock}
```

Templates are useful when one text layer should replace several separate labels.

---

# 8. Creating player stat and foul popups

Select **Screen → Stats**.

Stats are a family rather than a single layout. The **Subtype** selector allows you to edit the supported stat shapes.

Player layouts:

```text
player.json      fallback player layout
player_1.json    player + 1 stat value
player_school.json optional school graphic (School / Kentucky-style payload)
player_2.json    player + 2 stat values
player_3.json    player + 3 stat values
player_4.json    player + 4 stat values
player_5.json    player + 5 stat values
player_foul.json player-foul popup
```

Team layouts:

```text
team.json        fallback team layout
team_1.json      one-column team stat
team_2.json      two-column team stat
team_3.json      three-column team stat
```

The executable chooses the appropriate file for the event, so layouts in the same family should have a consistent visual identity.

## Player bindings

Useful player fields include:

```text
player.firstName
player.lastName
player.fullName
player.jerseyNumber
player.portrait
```

The editor includes a **Jersey #** button under Layers. It creates a text layer already bound to:

```text
player.jerseyNumber
```

The **Jersey #** field in Preview Data controls the number shown while designing.

## Stat/team bindings

Useful stat fields include:

```text
stat.teamName
stat.teamLogo
stat.teamColor
stat.primaryColor
stat.secondaryColor
stat.label1
stat.value1
stat.label2
stat.value2
```

The runtime payload can also be accessed directly with:

```text
stat.raw0
stat.raw1
stat.raw2
...
stat.raw14
```

The editor's **Stat values 0–14 (use |)** box provides those 15 raw preview values in order.

For the supplied player/foul sample, the beginning of the payload is used as:

```text
stat.raw0  first name
stat.raw1  last name
stat.raw2  first stat label
stat.raw3  first stat value
stat.raw4  second stat label
stat.raw5  second stat value
```

Later raw fields may carry event-specific values. When designing a new event type, use the runtime logger / known popup sample to determine which raw index corresponds to the value you want rather than assuming every stat event uses all 15 positions identically.

## Player portraits

A layer bound to:

```text
player.portrait
```

can display the featured player image when the runtime supplies a matching portrait. Keep portrait assets in the layout/theme structure expected by the plugin.

## Recommended stat-popup workflow

1. Open a known working player or team stat layout.
2. Choose the appropriate Stats subtype.
3. Design the common background first.
4. Add team color/logo elements.
5. Add player name and jersey number for player popups.
6. Add portrait if the theme uses portraits.
7. Add the needed `stat.rawN` labels/values.
8. Enter representative data in Preview Data.
9. Test short and long names.
10. Repeat the layout style across all required stat subtypes.

---


### Optional player school layout

`player_school.json` is a semantic override for the **Player school** stat used by NBA Live 2005/06. It is optional. When it exists, the runtime uses it specifically for the school popup. When it does not exist, the normal stat-family fallback continues to `player_1.json`, then `player.json`.

The layout can simply be a copy of `player_1.json`. A representative payload is:

```text
Tayshaun|Prince|School|Kentucky|||||||||4925563|ll|TAPRINC_
```

Useful bindings are the same as a one-value player stat:

```text
player.firstName   -> Tayshaun
player.lastName    -> Prince
stat.raw2          -> School
stat.raw3          -> Kentucky
```

For a single combined line, use:

```json
"binding": "",
"template": "{stat.raw2} {stat.raw3}",
"overflow": "fitWidth"
```

which renders as `School Kentucky`.

# 9. Creating violation popups

Select **Screen → Violation**.

The layout is stored at:

```text
violation\violation.json
```

Useful bindings are:

```text
violation.title
violation.possession
violation.teamName
violation.teamLogo
violation.teamColor
```

Preview fields include **Violation** and **Possession**.

A typical violation popup might show:

```text
DEFENSIVE FOUL
MINNESOTA BALL
```

along with the affected team's logo or color.

Violation overlays have their own overlay Z-order, so use the Layout tab if they need to appear above or below another active graphic.

---

# 10. Creating play-call popups

Select **Screen → Playcall**.

The layout is stored at:

```text
playcall\playcall.json
```

Useful bindings include:

```text
playcall.team
playcall.call
playcall.teamColor
```

The raw play-call payload can also be previewed through:

```text
playcall.raw0
playcall.raw1
playcall.raw2
playcall.raw3
```

The editor Preview Data has fields for:

- Play-call team
- Play call
- Play-call RGB

Use these to build possession/play-selection graphics that match the rest of the package.

---

# 11. Creating the game intro

Select **Screen → Intro**.

The layout is stored at:

```text
intro\intro.json
```

The intro has 15 preview payload values, entered in **Intro values 0–14 (use |)**.

Named intro bindings include:

```text
intro.homeHeading
intro.awayCity
intro.awayNickname
intro.awayRecord
intro.homeCity
intro.homeNickname
intro.homeRecord
intro.liveFromHeading
intro.arena
intro.location
intro.homeNumeric
intro.awayNumeric
intro.awayTeamCode
intro.homeTeamCode
intro.leagueCode
intro.awayLogo
intro.homeLogo
```

Equivalent direct payload access is available with:

```text
intro.raw0
...
intro.raw14
```

The current preview order is:

```text
0   home heading / package heading
1   away city
2   away nickname
3   away record
4   home city
5   home nickname
6   home record
7   live-from heading
8   arena
9   location
10  home numeric field
11  away numeric field
12  away team code
13  home team code
14  league code
```

A practical intro usually contains team names/logos, records, arena, and location. Use animation settings to make the package enter and leave like a broadcast graphic.

---

# 12. Creating starting-lineup graphics

Select **Screen → Starting Lineup**.

The file is:

```text
starting5\starting5.json
```

The starting lineup preview contains 11 values:

```text
0   player 1 ID/package
1   player 2 ID/package
2   player 3 ID/package
3   player 4 ID/package
4   player 5 ID/package
5   player 1 display name
6   player 2 display name
7   player 3 display name
8   player 4 display name
9   player 5 display name
10  team code
```

Named bindings include:

```text
starting5.player1Id
starting5.player2Id
starting5.player3Id
starting5.player4Id
starting5.player5Id

starting5.player1Name
starting5.player2Name
starting5.player3Name
starting5.player4Name
starting5.player5Name

starting5.player1FirstName
starting5.player1LastName
starting5.player1FullName
starting5.player1Number
starting5.player1JerseyNumber
...same FirstName/LastName/FullName/Number/JerseyNumber bindings for players 2–5

starting5.player1Portrait
starting5.player2Portrait
starting5.player3Portrait
starting5.player4Portrait
starting5.player5Portrait

starting5.teamCode
starting5.teamName
starting5.cityName
starting5.teamLogo
starting5.primaryColor
starting5.secondaryColor
starting5.side
```


The runtime resolves the abbreviated Starting 5 names against the live 24-player roster in NBA Live 07/08. The resolved bindings therefore expose the player's current first name, last name, full name, and jersey number without changing the original package/name bindings. In the editor, use **Starting5 resolved full names 1–5** and **Starting5 jersey numbers 1–5** under Preview Data to simulate these values.

Raw access is also available:

```text
starting5.raw0
...
starting5.raw10
```

## Starting-five portraits

For editor preview, portrait bindings look for images under:

```text
starting5\portraits\
```

using the player ID/package value as the filename stem, for example:

```text
starting5\portraits\ALIVERS.png
```

If your design does not use portraits, simply omit those image layers.

---

# 13. Creating the outro

Select **Screen → Outro**.

The layout is:

```text
outro\outro.json
```

The editor exposes 15 outro values.

Named bindings include:

```text
outro.homeHeading
outro.awayCity
outro.awayNickname
outro.awayRecord
outro.homeCity
outro.homeNickname
outro.homeRecord
outro.extra
outro.arena
outro.location
outro.awayScore
outro.homeScore
outro.awayTeamCode
outro.homeTeamCode
outro.leagueCode
outro.awayLogo
outro.homeLogo
outro.awayPrimaryColor
outro.awaySecondaryColor
outro.homePrimaryColor
outro.homeSecondaryColor
```

Raw access:

```text
outro.raw0
...
outro.raw14
```

The current preview order is:

```text
0   heading
1   away city
2   away nickname
3   away record
4   home city
5   home nickname
6   home record
7   extra field
8   arena
9   location
10  away score
11  home score
12  away team code
13  home team code
14  league code
```

This is suitable for final-score graphics and post-game presentation.

---

# 14. Creating in-game lineup graphics

Select **Screen → In-Game Lineups**.

The file is:

```text
lineups\lineups.json
```

The preview contains 14 values:

```text
0   away player 1
1   away player 2
2   away player 3
3   away player 4
4   away player 5
5   home player 1
6   home player 2
7   home player 3
8   home player 4
9   home player 5
10  away team code
11  away team name
12  home team code
13  home team name
```

Named bindings include:

```text
lineups.awayPlayer1
lineups.awayPlayer2
lineups.awayPlayer3
lineups.awayPlayer4
lineups.awayPlayer5
lineups.homePlayer1
lineups.homePlayer2
lineups.homePlayer3
lineups.homePlayer4
lineups.homePlayer5
lineups.awayTeamCode
lineups.awayTeamName
lineups.homeTeamCode
lineups.homeTeamName
lineups.awayLogo
lineups.homeLogo
lineups.awayPrimaryColor
lineups.awaySecondaryColor
lineups.homePrimaryColor
lineups.homeSecondaryColor
```

Raw access is available through `lineups.raw0` through `lineups.raw13`.

---

# 15. Team data and logos

The editor uses `teams.json` to populate its Away/Home preview selectors and to resolve team names, colors, short codes, and logos.

A team entry can contain fields such as:

```json
{
  "TEAMNUM": 1,
  "TEAMNAME": "Celtics",
  "CITYNAME": "Boston",
  "ABBREV": "BOS",
  "TEAMABR2": "bo",
  "PRIRGB": 30770,
  "SECRGB": 16119285,
  "logo": "teams/bo.png"
}
```

Colors are stored as decimal RGB integers.

Other overlays can reuse the scoreboard's `teams.json`, so you normally do not need to maintain a separate full team table for every folder.

---

# 16. Colors and team-color bindings

Many color fields accept a decimal RGB number.

For dynamic team-colored graphics, prefer a binding instead of hardcoding the color.

Examples:

```text
away.primaryColor
home.primaryColor
stat.teamColor
starting5.primaryColor
violation.teamColor
playcall.teamColor
```

A gradient can use bindings at either end. For example, one side can use the current team's primary color while the other side fades into a fixed dark color.

Use the color-picker buttons when available instead of calculating decimal RGB manually.

---

# 17. Fonts and popup.json

Font settings are stored in `popup.json` beside the relevant layout when present.

A basic font definition looks like:

```json
{
  "fontFile": "fonts/simian.otf",
  "fontFace": "SimianText-Chimpanzee",
  "fontWeight": 200,
  "characterSpacing": 1
}
```

Named presets are stored under `fonts`, for example:

```json
"fonts": {
  "teams": {
    "fontFile": "fonts/simian_italic.otf",
    "fontFace": "SimianText-ChimpanzeeItalic",
    "fontWeight": 400,
    "characterSpacing": 1
  }
}
```

Then an element can set its **Font preset** to:

```text
teams
```

If the Font preset is blank, the default popup font is used.

For best results, keep font files inside the theme package instead of relying on fonts installed only on your own Windows system.

---

# 18. Text sizing: overflow vs fit

Text boxes can behave in different ways.

## Overflow

The configured font size is preserved even if the text exceeds the element bounds.

Use this when typography must always remain a specific size and you already know the maximum expected text length.

## Fit

The renderer can reduce the text so that it fits inside the element bounds.

Use **fit** for variable data such as:

- Player names
- Team names
- Arena names
- Long stat labels

This prevents unusually long names from colliding with neighboring elements.

---

# 19. Text transform and small caps

Text layers support transformations such as uppercase. Small-caps scaling can be adjusted using **Small caps scale**.

These tools are useful for recreating broadcast packages where names are always uppercase or where lowercase letters should be rendered at a reduced height.

---

# 20. Stroke and shadow

Text can have both an outline and a hard-edged shadow.

The render order is:

1. Shadow
2. Stroke
3. Main text

Use stroke for readability over photographs or bright team colors. Use shadows sparingly to separate text from the underlying panel.

---

# 21. Z-order

Every layer has a **Z-order**.

Higher layers appear over lower layers.

A simple structure might be:

```text
0   background panel
1   accent graphics
2   team logos / portrait
3   text
4   foreground frame
```

There is also an overall **Overlay Z-order** in the Layout tab. That controls the relationship between entire overlays, not individual layers inside one overlay.

---

# 22. Using images correctly

Place theme graphics inside the popup package and use relative paths, for example:

```text
images/background.png
images/stats.png
teams/bo.png
fonts/myfont.otf
```

Relative paths make the theme portable to another installation.

Avoid absolute paths such as:

```text
C:\Users\YourName\Desktop\image.png
```

because they will not exist on another user's computer.

---

# 23. Save, Save As, and live reload

The toolbar contains:

- **Save** — saves the current JSON.
- **Save As...** — saves a copy to another path.
- **Save + Reload in Game** — saves and signals the ASI plugin to reload the popup package.

Recommended live workflow:

1. Start NBA Live.
2. Enter a game.
3. Pause the game.
4. Open the active popup layout in the editor.
5. Make your changes.
6. Click **Save + Reload in Game**.
7. Return to the game and inspect the result.
8. Repeat.

The editor writes/updates the theme's `.reload` marker. The plugin checks it periodically from the D3D9 render path.

`F5` remains available as a manual reload method in the supported launcher setup.

---

# 24. Building a completely new theme: recommended method

Do not begin with an empty directory unless you already understand the JSON format and plugin asset rules.

The easiest workflow is:

1. Copy a complete working popup theme.
2. Rename the copied theme folder.
3. Open its `scoreboard\scoreboard.json`.
4. Replace artwork and fonts.
5. Redesign the scoreboard.
6. Open each additional screen from the Screen selector.
7. Redesign Stats, Violation, Playcall, Intro, Starting Lineup, Outro, and Lineups as needed.
8. Keep bindings intact while changing visual style.
9. Test every layout in-game.
10. Remove only assets you have confirmed are no longer referenced.

This preserves required files and gives you working live bindings from the start.

---

# 25. Suggested order for designing a full broadcast package

For a new package, this order is efficient:

1. **Scoreboard** — establishes colors, fonts, logo treatment, and overall style.
2. **Player foul / Stats** — defines the lower-third language.
3. **Violation** — reuse the stat-popup style.
4. **Playcall** — reuse the same panel and typography.
5. **Intro** — build the larger pre-game presentation.
6. **Starting Lineup** — reuse intro assets and team identity.
7. **In-Game Lineups** — create a compact lineup presentation.
8. **Outro** — finish with the final-score/post-game graphic.

Reuse the same fonts, colors, margins, and animation timing throughout the package so every overlay appears to belong to the same broadcast theme.

---

# 26. Common mistakes

## The screen selector says the layout does not exist

The expected JSON file is missing from the corresponding theme subfolder. Check the folder names and filenames shown earlier in this guide.

## A live value is blank in the editor

Check the element's **Data binding** spelling and then check the corresponding Preview Data field.

## A live value is blank in game but visible in the editor

The selected event may not supply that field. This is particularly important for generic `stat.rawN` fields, whose contents depend on the event payload.

## The wrong stat design appears in game

Remember that Stats has multiple layout files. The executable selects a subtype such as `player_2.json` or `team_3.json`. Editing only `player.json` will not redesign every stat event.

## My jersey number is blank

For player stat/foul layouts, use:

```text
player.jerseyNumber
```

or add the layer using **Layers → Jersey #**.

## My image works only on my PC

Use a path relative to the theme folder, not an absolute Windows path.

## Text is cut off

Increase the element bounds or switch **Text overflow** to **fit**.

## An object cannot be dragged

It may be locked. Select it in the Layers tab and disable **Locked in editor**.

## An object is behind another element

Adjust its element Z-order or use Move Up / Move Down in the Layers tab.

## The popup appears behind another popup in game

Adjust the overall **Overlay Z-order** in the Layout tab.

---

# 27. Quick binding reference

## Main scoreboard

```text
away.logo                  home.logo
away.name                  home.name
away.score                 home.score
away.fouls                 home.fouls
away.timeouts              home.timeouts
away.bonus                 home.bonus
away.primaryColor          home.primaryColor
away.secondaryColor        home.secondaryColor
game.clock
game.shotClock
game.period
```

## Stats / player foul

```text
player.firstName
player.lastName
player.fullName
player.jerseyNumber
player.portrait
stat.teamName
stat.teamLogo
stat.teamColor
stat.primaryColor
stat.secondaryColor
stat.label1
stat.value1
stat.label2
stat.value2
stat.raw0 ... stat.raw14
```

## Violation

```text
violation.title
violation.possession
violation.teamName
violation.teamLogo
violation.teamColor
```

## Playcall

```text
playcall.team
playcall.call
playcall.teamColor
playcall.raw0 ... playcall.raw3
```

## Intro

```text
intro.homeHeading
intro.awayCity
intro.awayNickname
intro.awayRecord
intro.homeCity
intro.homeNickname
intro.homeRecord
intro.liveFromHeading
intro.arena
intro.location
intro.homeNumeric
intro.awayNumeric
intro.awayTeamCode
intro.homeTeamCode
intro.leagueCode
intro.awayLogo
intro.homeLogo
intro.raw0 ... intro.raw14
```

## Starting lineup

```text
starting5.player1Id ... starting5.player5Id
starting5.player1Name ... starting5.player5Name
starting5.player1Portrait ... starting5.player5Portrait
starting5.teamCode
starting5.teamName
starting5.cityName
starting5.teamLogo
starting5.primaryColor
starting5.secondaryColor
starting5.side
starting5.raw0 ... starting5.raw10
```

## Outro

```text
outro.homeHeading
outro.awayCity
outro.awayNickname
outro.awayRecord
outro.homeCity
outro.homeNickname
outro.homeRecord
outro.extra
outro.arena
outro.location
outro.awayScore
outro.homeScore
outro.awayTeamCode
outro.homeTeamCode
outro.leagueCode
outro.awayLogo
outro.homeLogo
outro.awayPrimaryColor
outro.awaySecondaryColor
outro.homePrimaryColor
outro.homeSecondaryColor
outro.raw0 ... outro.raw14
```

## In-game lineups

```text
lineups.awayPlayer1 ... lineups.awayPlayer5
lineups.homePlayer1 ... lineups.homePlayer5
lineups.awayTeamCode
lineups.awayTeamName
lineups.homeTeamCode
lineups.homeTeamName
lineups.awayLogo
lineups.homeLogo
lineups.awayPrimaryColor
lineups.awaySecondaryColor
lineups.homePrimaryColor
lineups.homeSecondaryColor
lineups.raw0 ... lineups.raw13
```

---

# 28. Final checklist before releasing a theme

- Open every supported screen in the editor.
- Test multiple away/home teams.
- Test long and short team names.
- Test long player names.
- Test jersey numbers with one and two digits.
- Test low and high scores.
- Test game clock and shot clock edge cases.
- Test all stat subtypes used by your package.
- Test regulation period and overtime presentation.
- Verify images use relative paths.
- Verify fonts are included in the package.
- Verify hidden development/reference images are not required at runtime.
- Test Save + Reload in Game.
- Restart the game once and verify the package also loads correctly from a clean launch.

Once all of these work, the popup package is ready to distribute.

---

# 26. Sample stat data strings

The stat layouts are easiest to test when you have known sample payloads that match each stat family. The examples below use pipe-separated values so they can be copied directly into your test/debug workflow.

## Player stat field order

The player stat samples use this logical order:

```text
firstName|lastName|label1|value1|label2|value2|label3|value3|label4|value4|label5|value5|teamColor|teamCode|portraitId
```

Not every subtype uses every label/value pair. The numbered player layouts simply stop after the number of stat pairs they support.

### Player fallback — `player.json`

```text
Lamar|Odom|Pts|18|Reb|10|Ast|6|Stl|2|Blk|1|4925563|ll|LAODOM_
```

### Player — 1 stat — `player_1.json`

```text
Lamar|Odom|Pts|18|4925563|ll|LAODOM_
```

### Player — 2 stats — `player_2.json`

```text
Lamar|Odom|Pts|18|Reb|10|4925563|ll|LAODOM_
```

### Player — 3 stats — `player_3.json`

```text
Lamar|Odom|Pts|18|Reb|10|Ast|6|4925563|ll|LAODOM_
```

### Player — 4 stats — `player_4.json`

```text
Lamar|Odom|Pts|18|Reb|10|Ast|6|Stl|2|4925563|ll|LAODOM_
```

### Player — 5 stats — `player_5.json`

```text
Lamar|Odom|Pts|18|Reb|10|Ast|6|Stl|2|Blk|1|4925563|ll|LAODOM_
```

### Player foul — `player_foul.json`

```text
Lamar|Odom|PF|3|TF|4|4925563|ll|LAODOM_
```

The player foul layout can also use the jersey-number binding introduced by the runtime:

```text
player.jerseyNumber
```

For example, a text layer can display the jersey number by itself:

```json
{
  "id": "playerJerseyNumber",
  "type": "text",
  "binding": "player.jerseyNumber",
  "x": 20,
  "y": 20,
  "width": 60,
  "height": 30,
  "alignment": "center",
  "overflow": "fitWidth",
  "fontHeight": 26
}
```

## Team stat field order

The team stat samples use this logical order:

```text
title|header1|header2|header3|row1Label|row1Value1|row1Value2|row1Value3|row2Label|row2Value1|row2Value2|row2Value3|teamColor|teamCode
```

### Team fallback — `team.json`

```text
Team Comparison|BOS|LAL|FT|FG|38/79|35/82|18/21|3PT|9/22|7/21|15/19|4925563|ll
```

### Team — 1 column — `team_1.json`

```text
Points in Paint|BOS|LAL||Points in Paint|42|34||Bench Pts|28|19||4925563|ll
```

### Team — 2 columns — `team_2.json`

```text
Team Comparison|BOS|LAL||FG|38/79|35/82||3PT|9/22|7/21||4925563|ll
```

### Team — 3 columns — `team_3.json`

```text
Team Comparison|BOS|LAL|FT|FG|38/79|35/82|18/21|3PT|9/22|7/21|15/19|4925563|ll
```

## Combining several stat values into one text layer

A stat board does not need a separate text element for every label and value. The **Text template** field can concatenate several bindings into one line.

For player stat layouts, the established raw-value pattern is:

```text
stat.raw2   first label
stat.raw3   first value
stat.raw4   second label
stat.raw5   second value
stat.raw6   third label
stat.raw7   third value
stat.raw8   fourth label
stat.raw9   fourth value
stat.raw10  fifth label
stat.raw11  fifth value
```

### One stat

```json
"template": "{stat.raw2} {stat.raw3}"
```

Result:

```text
Pts 18
```

### Two stats

```json
"template": "{stat.raw2} {stat.raw3}, {stat.raw4} {stat.raw5}"
```

Result:

```text
Pts 18, Reb 10
```

### Three stats

```json
"template": "{stat.raw2} {stat.raw3}, {stat.raw4} {stat.raw5}, {stat.raw6} {stat.raw7}"
```

Result:

```text
Pts 18, Reb 10, Ast 6
```

### Four stats

```json
"template": "{stat.raw2} {stat.raw3}, {stat.raw4} {stat.raw5}, {stat.raw6} {stat.raw7}, {stat.raw8} {stat.raw9}"
```

Result:

```text
Pts 18, Reb 10, Ast 6, Stl 2
```

### Five stats

```json
"template": "{stat.raw2} {stat.raw3}, {stat.raw4} {stat.raw5}, {stat.raw6} {stat.raw7}, {stat.raw8} {stat.raw9}, {stat.raw10} {stat.raw11}"
```

Result:

```text
Pts 18, Reb 10, Ast 6, Stl 2, Blk 1
```

For long combined strings, use:

```json
"overflow": "fitWidth"
```

This keeps the configured text height and compresses the line horizontally only when it is too wide for its element bounds.

## Combining foul values

The player-foul path also exposes named stat bindings, so the two foul values can be combined cleanly:

```json
"template": "{stat.label1} {stat.value1}, {stat.label2} {stat.value2}"
```

Example result:

```text
PF 3, TF 4
```

## More useful test combinations

The following combinations are useful when testing different text lengths and layouts:

```text
Pts|31
Reb|14
Ast|11
Stl|4
Blk|5
```

```text
Pts|22|Reb|10
Pts|18|Ast|9
Stl|3|Blk|2
```

```text
Pts|27|Reb|11|Ast|7
FGM|9|FGA|16|FG%|56%
```

```text
Pts|25|Reb|9|Ast|6|Stl|3
```

```text
Pts|28|Reb|12|Ast|8|Stl|2|Blk|2
```

For team layouts, useful categories include:

```text
Points in Paint
Fast Break Points
Bench Points
Second Chance Points
```

and multi-column comparisons such as:

```text
FG | 38/79 | 35/82
3PT | 9/22 | 7/21
FT | 18/21 | 15/19
```

These samples are intended as predictable test payloads for building and validating layouts. Replace the labels, values, colors, team codes, and portrait IDs with whatever the game sends for the popup you are reproducing.

---

# Team identity lookup from stat payloads

Team stat payloads sometimes contain team identity as text instead of a database
team ID or logo code. The editor/runtime can resolve those values through the
theme's `scoreboard\teams.json`.

For example:

```text
Field Goals||||Minnesota|6-6|||Phoenix|5-6|||149632|le
```

For this payload the useful raw fields are:

```text
stat.raw0   Field Goals
stat.raw4   Minnesota
stat.raw5   6-6
stat.raw8   Phoenix
stat.raw9   5-6
stat.raw12  149632
stat.raw13  le
```

The team resolver scans the populated stat payload values and looks for exact
matches in `teams.json`. Matching accepts `ABBREV`, `TEAMABR2`, `CITYNAME`,
`TEAMNAME`, or the full `CITYNAME + TEAMNAME`. The first two distinct matched
teams become the left and right stat teams.

For the example above:

```text
Minnesota -> left team
Phoenix   -> right team
```

City and nickname matching must be unambiguous. If a value such as
`Los Angeles` matches more than one team, the resolver does not guess.

## Team-stat bindings

Image bindings:

```text
stat.leftTeamLogo
stat.rightTeamLogo
```

Text bindings:

```text
stat.leftTeamCity
stat.leftTeamName
stat.leftTeamNickname
stat.leftTeamAbbreviation
stat.leftTeamShortCode
stat.leftTeamFullName

stat.rightTeamCity
stat.rightTeamName
stat.rightTeamNickname
stat.rightTeamAbbreviation
stat.rightTeamShortCode
stat.rightTeamFullName
```

`stat.leftTeamName` and `stat.rightTeamName` use `TEAMNAME`. `...City` uses
`CITYNAME`.

Color bindings:

```text
stat.leftTeamPrimaryColor
stat.leftTeamSecondaryColor
stat.rightTeamPrimaryColor
stat.rightTeamSecondaryColor
```

Example logo layer:

```json
{
  "id": "leftLogo",
  "type": "image",
  "binding": "stat.leftTeamLogo",
  "x": 20,
  "y": 45,
  "width": 64,
  "height": 64,
  "imageFit": "contain"
}
```

Example team-color panel:

```json
{
  "id": "leftPanel",
  "type": "rectangle",
  "x": 0,
  "y": 35,
  "width": 280,
  "height": 80,
  "fill": {
    "type": "solid",
    "binding": "stat.leftTeamPrimaryColor",
    "color": 0
  }
}
```

The automatic team lookup is independent of the raw-field bindings. You can
still display `stat.raw4` and `stat.raw8` exactly as the game sent them while
using `stat.leftTeamLogo` and `stat.rightTeamLogo` for resolved graphics.

## Team Leaders player/team bindings

`team_leaders.json` supports player-specific Team Leaders bindings:

```text
player1.name
player1.value
player1.teamLogo
player1.teamColor
player1.teamPrimaryColor
player1.teamSecondaryColor

player2.name
player2.value
player2.teamLogo
player2.teamColor
player2.teamPrimaryColor
player2.teamSecondaryColor
```

For editor preview, `player1.name/value` use `stat.raw4/raw5` and
`player2.name/value` use `stat.raw8/raw9`.

The running game resolves each leader's team independently from the 24-player
cache, so row order does not mean home or away. The editor cannot access that
live cache, so preview uses the selected Away team for `player1.team*` and the
selected Home team for `player2.team*`.

The Layers tab includes **Leader 1 Logo** and **Leader 2 Logo** buttons. These
create movable image layers already bound to `player1.teamLogo` and
`player2.teamLogo`. Exact position and size can then be changed in the Element
tab like any other layer.



### Starting 5 resolved positions

The Starting 5 runtime exposes fixed positional bindings matching the payload row order:

```text
starting5.player1Position = PG
starting5.player2Position = SG
starting5.player3Position = SF
starting5.player4Position = PF
starting5.player5Position = C
```

For NBA Live 07/08, resolved Starting 5 identity uses the payload team plus the engine's starter roster-slot order `4, 3, 2, 1, 0` as the primary key. Abbreviated player-name matching is retained only as a same-team fallback.

## Shared season-comparison stat layout

The following semantic stat subtypes share one optional layout file:

```text
season_assists
season_blocks
season_rebounds
season_steals
```

Shared file:

```text
stats\season_comparison.json
```

Runtime lookup order remains:

1. Exact subtype file, for example `season_rebounds.json`
2. Shared `season_comparison.json`
3. Generic `team_N.json`
4. Generic `team.json`

The observed 14-value season-comparison payload shape is:

```text
raw0  = stat title         (example: Rebounds)
raw4  = left label         (Season)
raw5  = left value         (43.8)
raw8  = right label        (Tonight)
raw9  = right value        (23)
raw12 = packed team color
raw13 = team code          (example: nj)
```

Because `raw13` is a team code, ordinary team stat bindings such as
`stat.teamLogo`, `stat.teamName`, `stat.teamColor`, `stat.primaryColor`, and
`stat.secondaryColor` remain available. Raw bindings can be used for the
comparison labels and values.
