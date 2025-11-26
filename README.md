# Ruffle Launcher

A self-contained, all-in-one Flash game launcher built with [Ruffle](https://ruffle.rs/). Designed for easy deployment and iframe embedding, making it perfect for creating Flash game widgets in applications like Nextcloud.

---

## ⚠️ **IMPORTANT NOTICE** ⚠️

**THIS PROJECT CONTAINS NO COPYRIGHTED SWF FILES OR FLASH CONTENT.**

This repository contains **ONLY** HTML, CSS, and JavaScript code that provides an interface for loading remote SWF files. The launcher itself does not host, distribute, or include any Flash games or copyrighted content. All game files are referenced from external sources (primarily Archive.org) and are loaded dynamically at runtime.

**Users are responsible for ensuring they have proper rights and permissions to access any remote SWF files they load through this launcher.**

---

## Features

- **All-in-One File**: Everything is contained in a single HTML file for maximum portability
- **Remote Game Support**: Load Flash games from any CORS-enabled URL
- **Clean, Modern UI**: Material Design 3-inspired interface with dark theme
- **Game Library**: Pre-loaded with popular Flash games (Club Penguin, Papa's Games, etc.)
- **Custom Games**: Add and manage your own game collection
- **Recently Played**: Quick access to your last 3 games
- **Search**: Global search across all game categories
- **Resolution Control**: Flexible resolution settings with presets
- **View Modes**: Fill Window and fullscreen support
- **Privacy Controls**: Clear all launcher data with one click
- **URL Parameters**: Extensive URL customization options for embedding

## Quick Installation

Deploy the launcher with a single command:

```bash
# Create directory
sudo mkdir -p /var/www/html/ruffle

# Download the launcher
sudo curl -o /var/www/html/ruffle/ruffle_launcher.html https://gitlab.com/nickgirga/ruffle-launcher/-/raw/master/public/index.html
```

The launcher will then be accessible at:
```
https://yourdomain.com/ruffle/ruffle_launcher.html
```

## URL Parameters

The launcher supports several URL parameters for customization:

### `file`
Load a specific SWF file directly on launch.

**Example:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?file=https://example.com/game.swf
```

### `width` and `height`
Set the dimensions of the Flash container (default: 800x600).

**Example:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?width=1024&height=768
```

### `drawerButton`
Control visibility of the menu drawer button. Set to `false` to hide it (default: visible).

**Example:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?drawerButton=false
```

This is useful when embedding in iframes where you want a cleaner appearance.

### `customResOption`
Specify a custom resolution preset to appear in the resolution dropdown.

**Example:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?customResOption=1920x1080
```

### Combining Parameters
You can combine multiple parameters using `&`:

**Example:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?file=https://example.com/game.swf&width=1024&height=768&drawerButton=false
```

## Using the Launcher

### Opening the Menu
- **Click** the hamburger menu button (☰) in the top-left corner
- **Keyboard shortcut**: `Ctrl+Alt+Shift+R`

### Searching for Games
1. Open the menu drawer
2. Type in the search bar at the top
3. Results update in real-time across all categories

### Playing a Game
1. Open the menu drawer
2. Browse or search for a game
3. Click the game button to load it
4. The game will load and the drawer will close automatically

### Adding Custom Games
1. Open the menu drawer
2. Scroll to the "Custom Games" section
3. Enter the game name and SWF URL
4. Click "Add"
5. Your custom game will appear in the Custom Games list

### Deleting Custom Games
1. Hover over a custom game button
2. Click the red × button that appears in the top-right corner
3. Confirm deletion

### Loading a Temporary SWF
For one-time testing without saving to your library:

1. Open the menu drawer
2. Scroll to "Load Custom SWF (temporary)"
3. Paste the SWF URL
4. Click "Load"

### Changing Resolution
1. Open the menu drawer
2. Scroll to the "Resolution" section
3. Either:
   - Type a custom resolution (e.g., `1280x720`)
   - Select a preset from the dropdown
4. Click "Apply"

### View Modes

**Fill Window**: Expands the game to fill your entire browser window
- Click "Fill Window" button to activate
- Click "Exit Fill Window" to restore original size

**Fullscreen**: Enter browser fullscreen mode
- Click "Fullscreen" to enter
- Click "Exit Fullscreen" (or press `Esc`) to exit

### Privacy

**Clear All Data**: Removes all launcher data from your browser
- Deletes recently played history
- Removes all custom games
- Click the "Clear All Data" button and confirm

## Nextcloud Integration

The Ruffle Launcher is ideal for use with the [Nextcloud iFrame Widget app](https://apps.nextcloud.com/apps/files_iframe), allowing you to have a Flash game launcher widget on your Nextcloud dashboard.

### Setup Instructions

1. **Install the iFrame Widget app** in Nextcloud:
   - Go to Apps → Office & text
   - Find "iFrame Widget" and install it

2. **Deploy the Ruffle Launcher** on your server:
   ```bash
   sudo mkdir -p /var/www/html/ruffle
   sudo curl -o /var/www/html/ruffle/ruffle_launcher.html https://gitlab.com/nickgirga/ruffle-launcher/-/raw/master/public/index.html
   ```

3. **Add the widget to your Nextcloud dashboard**:
   - Go to your Nextcloud dashboard
   - Click "Customize"
   - Add the "iFrame Widget"

4. **Configure the widget**:
   - **URL**: `https://yourdomain.com/ruffle/ruffle_launcher.html`
   - **Optional**: Add URL parameters for customization:
     ```
     https://yourdomain.com/ruffle/ruffle_launcher.html?width=900&height=600&drawerButton=true
     ```

5. **Adjust widget size** on the dashboard to your preference

### Recommended Settings for Nextcloud

For the best experience in a Nextcloud widget:

**URL:**
```
https://yourdomain.com/ruffle/ruffle_launcher.html?width=640&height=405&customResOption=640x405
```

**Widget Settings:**
- **Width**: `Extra Wide (2 Col)`
- **iFrame Height**: `100%` (default, leave empty)

This provides a good balance between visibility and dashboard space usage.

## Browser Compatibility

The launcher includes automatic browser detection:
- **Firefox/Waterfox**: Automatically uses Canvas renderer for better compatibility
- **Other browsers**: Uses WebGL renderer for improved performance

Ruffle itself supports all modern browsers. For the best experience, use an up-to-date version of:
- Chrome/Chromium
- Firefox
- Safari
- Edge

## Working with CORS-Enabled URLs

### What is CORS?

**CORS (Cross-Origin Resource Sharing)** is a security mechanism that browsers use to restrict web pages from making requests to a different domain than the one serving the page. For this launcher to load SWF files from remote sources, those files must be served with proper CORS headers that allow cross-origin access.

**Important**: Not all websites allow CORS access to their files. If you try to load a SWF from a non-CORS-enabled source, the browser will block it and you'll see an error in the console.

### Using Archive.org (Internet Archive)

Archive.org is one of the best sources for finding CORS-enabled SWF files. They provide a special CORS endpoint that makes files accessible to web applications like this launcher.

#### How to Get CORS-Enabled URLs from Archive.org

Archive.org uses a specific URL structure for CORS-enabled downloads. Here's how to convert a regular download URL to a CORS-enabled one:

**Standard Download URL format:**
```
https://archive.org/download/[collection-name]/[file-name].swf
```

**CORS-Enabled URL format:**
```
https://archive.org/cors/[collection-name]/[file-name].swf
```

**The key difference**: Replace `download` with `cors` in the URL.

#### Step-by-Step: Finding and Converting Archive.org URLs

1. **Find a SWF file on Archive.org**:
   - Go to [https://archive.org](https://archive.org)
   - Search for Flash games or SWF files
   - Click on a collection/item that interests you

2. **Navigate to the download page**:
   - Click "Show All" or "Download Options" to see all files
   - Find the `.swf` file you want to use

3. **Get the download URL**:
   - **Right-click** on the SWF file link
   - Select "Copy Link Address" (or similar option in your browser)
   - The URL will look like this:
     ```
     https://archive.org/download/pizzatron-3000/Pizzatron3000.swf
     ```

4. **Convert to CORS URL**:
   - Paste the URL somewhere (text editor, browser address bar, etc.)
   - Replace `download` with `cors`:
     ```
     https://archive.org/cors/pizzatron-3000/Pizzatron3000.swf
     ```

5. **Use the CORS URL**:
   - This converted URL can now be used in the launcher
   - Paste it into the "Load Custom SWF" field, or
   - Add it as a custom game with a name

#### Example Conversion

**Original Download URL:**
```
https://archive.org/download/papasgamesarchive/papasburgeria.swf
```

**CORS-Enabled URL:**
```
https://archive.org/cors/papasgamesarchive/papasburgeria.swf
```

Simply change `download` → `cors`. That's it!

#### URL Encoding

Note that file names with spaces or special characters will be URL-encoded (spaces become `%20`, etc.). This is automatic and normal. For example:
- `Game Name.swf` becomes `Game%20Name.swf`

The CORS conversion works the same way regardless of encoding.

### Other CORS-Enabled Sources

While Archive.org is the most reliable source for CORS-enabled SWF files, you may find other sources that support CORS. To test if a URL is CORS-enabled:

1. Try loading it in the launcher
2. Check the browser's Developer Console (F12) for CORS errors
3. If you see errors like "blocked by CORS policy," the file is not accessible

**Note**: This limitation exists only for Archive.org URLs. The `download` → `cors` conversion is specific to Archive.org's infrastructure and will not work on other websites.

## Game Library

The launcher comes pre-loaded with several categories:

### Classics
- Sushi Cat 2, Age of War, Bloxors

### PSA Missions
- PSA Mission 1-4 (Club Penguin)

### Club Penguin
- Hydro Hopper, Aqua Grabber, Bean Counters, Catchin' Waves, Cart Surfer, Jet Pack Adventure, Ice Fishing, Pizzatron 3000, DJ3K

### Papa's Games & Friends
- Full collection of Papa Louie games, including platformers and restaurant management games
- Cactus McCoy series, Jacksmith, and more

All games are loaded from Internet Archive's CORS-enabled endpoints.

## Data Storage

The launcher uses browser localStorage to save:
- Recently played games (last 3)
- Custom game library
- No data is sent to external servers

You can clear all stored data using the "Clear All Data" button in the View & Privacy section.

## Technical Details

- **Framework**: Vanilla JavaScript (no dependencies)
- **Flash Emulator**: Ruffle (latest stable build from unpkg CDN)
- **File Size**: ~40KB (single HTML file)
- **External Resources**: Only loads Ruffle library from CDN
- **CORS**: Games must be served from CORS-enabled domains

## License

This project is free and open source. Ruffle is licensed under Apache 2.0 and MIT licenses.

## Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

## Credits

- [Ruffle](https://ruffle.rs/) - Flash Player emulator
- Game SWF files courtesy of [Internet Archive](https://archive.org/)
