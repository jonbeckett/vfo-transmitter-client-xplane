# Transmitter XP

A FlyWithLua plugin for X-Plane 11 and X-Plane 12 that transmits real-time aircraft position data to a Transmitter server for flight tracking and sharing. This enables X-Plane pilots to participate in shared tracking networks, group flights, and virtual ATC sessions.

## 🎯 Overview

**Transmitter XP** is part of the Virtual Flight Online Transmitter ecosystem, enabling flight simulator enthusiasts to share their real-time aircraft positions with friends for group flights and air traffic control sessions. The system transmits aircraft telemetry data to a web server, which provides multiple viewing interfaces including an interactive radar display and IVAO-compatible data feeds for applications like LittleNavMap.

### Why Use This?

X-Plane only communicates AI aircraft to external mapping applications like LittleNavMap - not other human pilots. This plugin bridges that gap, allowing you to:

- 👥 See your friends' aircraft positions in real-time
- 🎙️ Run your own air traffic control sessions
- ✈️ Coordinate group flights with live tracking
- 🗺️ Monitor multiple aircraft on interactive web-based radar displays
- 📡 Share your position with LittleNavMap users via IVAO-compatible feeds

## ✨ Features

- **Real-time Position Transmission**: Broadcasts position data every second
- **Persistent HTTP Connection**: Efficient data transmission with connection reuse
- **Comprehensive Telemetry**: Transmits aircraft type, position, altitude, heading, airspeed, groundspeed, transponder code, and touchdown velocity
- **ImGui User Interface**: Modern, interactive configuration window
- **Persistent Configuration**: Settings automatically saved between sessions
- **Automatic Landing Detection**: Tracks and reports touchdown velocity
- **Cross-Platform Support**: Works on Windows, macOS, and Linux
- **Auto-Connect Option**: Connect and hide at startup for seamless integration
- **Text-to-Speech Feedback**: Audio confirmation of connection status
- **Automatic Reconnection**: Handles connection drops gracefully

## 📋 Requirements

- **X-Plane 11** or **X-Plane 12**
- **FlyWithLua plugin** (NG or NG+ edition)
- **LuaSocket** (typically included with FlyWithLua)
- **Active internet connection**
- **Transmitter server** (self-hosted or shared)

## 📥 Installation

### Step 1: Install FlyWithLua Plugin

If you don't already have FlyWithLua installed:

1. **Download FlyWithLua**:
   - Visit [X-Plane.org FlyWithLua page](https://forums.x-plane.org/index.php?/files/file/38445-flywithlua-ng-next-generation-edition-for-x-plane-11-win-lin-mac/)
   - Download the appropriate version for your platform and X-Plane version

2. **Extract the archive**:
   - You'll get a folder named `FlyWithLua` or similar

3. **Install to X-Plane**:
   - Copy the `FlyWithLua` folder to your X-Plane plugins directory:
     - **Windows**: `C:\X-Plane 12\Resources\plugins\`
     - **macOS**: `/Applications/X-Plane 12/Resources/plugins/`
     - **Linux**: `~/X-Plane 12/Resources/plugins/`
   - Final path should be: `X-Plane/Resources/plugins/FlyWithLua/`

4. **Verify installation**:
   - Launch X-Plane
   - Check **Plugins** menu - you should see **FlyWithLua** listed

### Step 2: Install Transmitter XP Script

1. **Download the script**:
   - Get `transmitter_xp.lua` from this repository

2. **Copy to Scripts folder**:
   - Place `transmitter_xp.lua` in:
     - **Windows**: `X-Plane 12\Resources\plugins\FlyWithLua\Scripts\`
     - **macOS**: `X-Plane 12/Resources/plugins/FlyWithLua/Scripts/`
     - **Linux**: `X-Plane 12/Resources/plugins/FlyWithLua/Scripts/`
   - The file should be directly in the Scripts folder, not in a subfolder

3. **Reload scripts** (choose one method):
   - **Option A**: Restart X-Plane completely
   - **Option B**: In X-Plane, go to **Plugins → FlyWithLua → Reload all Lua script files**

4. **Verify installation**:
   - Go to **Plugins → FlyWithLua → Macros**
   - You should see **"Transmitter XP: Show Window"** in the list

## 🚀 Usage

### Opening the Transmitter XP Window

Choose one of these methods:

**Method 1: From the Plugins Menu**
1. Click on **Plugins** in the X-Plane menu bar
2. Navigate to **FlyWithLua → Macros**
3. Click on **Transmitter XP: Show Window**

**Method 2: From the FlyWithLua Macros Menu**
1. Click on **Plugins** in the X-Plane menu bar
2. Navigate to **FlyWithLua → FlyWithLua Macros**
3. Select **Transmitter XP: Show Window**

The Transmitter XP window will appear on your screen.

### First-Time Configuration

Before your first flight, configure the following settings in the Transmitter XP window:

| Field | Description | Example |
|-------|-------------|---------|
| **Server URL** | The transmitter server endpoint | `http://yourserver/transmitter/transmit` |
| **Callsign** | Your aircraft callsign | `N12345`, `AAL123`, `GABCD` |
| **Pilot Name** | Your name or username | `John Doe` |
| **Group Name** | Organization/group identifier | `VirtualFlight.Online` |
| **PIN** | Server authentication PIN (if required) | `1234` |
| **Notes** | Optional flight notes | `Training flight` |

> **Note**: Configuration fields are editable only when disconnected. Once connected, they display as read-only text.

### Starting Transmission

1. Configure your settings (see above)
2. Click the **Connect** button
3. Your settings are automatically saved to `X-Plane/Output/preferences/transmitter_xp_config.txt`
4. The button will change to **Disconnect**
5. You'll hear "Connected to Transmitter server" via text-to-speech
6. Your position data will now be transmitted every second to the server

### Stopping Transmission

1. Click the **Disconnect** button
2. The button will change back to **Connect**
3. Position transmission will stop
4. Configuration fields become editable again

### Auto-Connect at Startup

For seamless integration:

1. Configure all your settings
2. Check the **"Connect and hide at startup"** checkbox
3. On next X-Plane launch, the plugin will automatically connect and remain hidden
4. To access settings later, use **Plugins → FlyWithLua → Macros → Transmitter XP: Show Window**

> **Important**: Auto-connect requires a valid callsign (not the default "CALLSIGN") and server URL.

### During Flight

- The window can remain open or be closed - transmission continues either way
- Status displays "Connected - Sending data every second" when active
- Touchdown velocity is shown and transmitted after each landing
- To stop transmitting, reopen the window and click **Disconnect**

## 📡 Transmitted Data

The plugin transmits the following aircraft telemetry to the server:

| Data Field | Description | Units |
|------------|-------------|-------|
| **Aircraft ICAO** | Aircraft type code from X-Plane dataref | Code (e.g., B738, C172) |
| **Latitude** | Current latitude position | Decimal degrees |
| **Longitude** | Current longitude position | Decimal degrees |
| **Altitude** | Elevation above sea level | Feet |
| **Indicated Airspeed** | IAS from cockpit instruments | Knots |
| **Ground Speed** | Speed over ground | Knots |
| **Heading** | True heading | Degrees |
| **Transponder Code** | Squawk code | 4-digit code |
| **Touchdown Velocity** | Vertical speed at landing | Feet per minute |
| **Callsign** | Your configured callsign | Text |
| **Pilot Name** | Your configured pilot name | Text |
| **Group Name** | Your configured group | Text |
| **PIN** | Server authentication | Text |
| **Notes** | Flight notes | Text |

## 🗺️ Viewing Your Position

### Web-Based Radar

If your server includes the radar component, view aircraft at:
- **Full Radar**: `http://yourserver/transmitter/radar.php`
- **Embeddable Radar**: `http://yourserver/transmitter/embed.php`
- **Status Dashboard**: `http://yourserver/transmitter/status.php`

### LittleNavMap Integration

To view aircraft positions in LittleNavMap:

1. Open LittleNavMap
2. **Tools → Options**
3. Select **Online Flying** section
4. Choose **Custom** radio button
5. Enter URL: `http://yourserver/transmitter/ivao.php`
6. Set update rate: **5 seconds**
7. Format dropdown: **IVAO**
8. Click **Apply** and **OK**

LittleNavMap will now display all active aircraft transmitting to the server.

## 🔧 Troubleshooting

### Window Doesn't Appear

- Ensure FlyWithLua plugin is properly installed and enabled
- Check the X-Plane `Log.txt` for any Lua script errors
- Try reloading Lua scripts: **Plugins → FlyWithLua → Reload all Lua script files**
- Verify the script file is in the correct Scripts folder (not in a subfolder)

### Cannot Connect / Connection Failed

- Verify your internet connection is active
- Ensure the Server URL is correct and includes the full path (e.g., `/transmit`)
- Check that the server is online and accessible
- If PIN is required by server, ensure it matches exactly
- You'll hear "Failed to connect" via text-to-speech with error details

### Data Not Transmitting

- Verify connection status shows "Connected" in the window
- Check that LuaSocket is properly installed with FlyWithLua
- Try disconnecting and reconnecting to re-establish the connection
- Check X-Plane's `Log.txt` for error messages (search for "Transmitter XP")
- Ensure the server hasn't rate-limited your IP

### Configuration Not Saving

- Ensure X-Plane has write permissions to the `Output/preferences/` folder
- Check that the folder exists: `X-Plane/Output/preferences/`
- On macOS/Linux, check file permissions

### LuaSocket Errors

- Reinstall FlyWithLua - LuaSocket should be included
- Verify LuaSocket files exist in the FlyWithLua installation
- Check for conflicts with other Lua scripts

### Performance Issues

The plugin is designed to be lightweight with minimal impact on X-Plane performance:

- Transmission occurs only once per second
- Uses persistent HTTP connection to reduce overhead (HTTP/1.1 keep-alive)
- Non-blocking I/O with 200ms connection timeout prevents simulator frame drops
- Connection is automatically reused for efficiency
- Disconnect when not needed to free resources

## 📁 File Locations

| File | Location | Purpose |
|------|----------|---------|
| Script | `X-Plane/Resources/plugins/FlyWithLua/Scripts/transmitter_xp.lua` | Main plugin script |
| Config | `X-Plane/Output/preferences/transmitter_xp_config.txt` | Saved settings |
| Log | `X-Plane/Log.txt` | Error messages (search for "Transmitter XP") |

## 🗑️ Uninstallation

To remove Transmitter XP:

1. Delete `transmitter_xp.lua` from the Scripts folder:
   - `X-Plane/Resources/plugins/FlyWithLua/Scripts/transmitter_xp.lua`
2. (Optional) Delete the configuration file:
   - `X-Plane/Output/preferences/transmitter_xp_config.txt`
3. Restart X-Plane or reload Lua scripts

## ⚙️ Technical Details

### Data Transmission Protocol

| Aspect | Details |
|--------|---------|
| **Method** | HTTP GET request over persistent TCP connection |
| **Format** | URL-encoded query parameters |
| **Frequency** | Once per second when connected |
| **Connection** | HTTP/1.1 with keep-alive |
| **Connect Timeout** | 200ms (prevents blocking) |
| **Send Mode** | Non-blocking (zero timeout) |
| **Library** | LuaSocket for TCP/HTTP communication |

### Connection Management

The plugin maintains a persistent TCP connection to the server:
- Connection is established when you click "Connect"
- Same connection is reused for all transmissions (efficient)
- Automatic reconnection attempt if connection drops
- Reconnection logged to X-Plane log with status messages
- Connection is properly closed when you click "Disconnect"

### Landing Detection

The plugin automatically detects landings by monitoring the `sim/flightmodel/failures/onground_any` dataref:
- Touchdown detected on transition from airborne to ground
- Vertical speed captured at moment of touchdown
- Only records if vertical speed exceeds 10 FPM (filters out already-settled aircraft)
- Touchdown velocity reset when taking off

### X-Plane Datarefs Used

| Dataref | Purpose |
|---------|---------|
| `sim/aircraft/view/acf_ICAO` | Aircraft type code |
| `sim/flightmodel/position/latitude` | Latitude position |
| `sim/flightmodel/position/longitude` | Longitude position |
| `sim/flightmodel/position/elevation` | Altitude (meters) |
| `sim/flightmodel/position/indicated_airspeed` | Indicated airspeed |
| `sim/flightmodel/position/groundspeed` | Ground speed (m/s) |
| `sim/flightmodel/position/psi` | True heading |
| `sim/cockpit/radios/transponder_code` | Transponder squawk |
| `sim/flightmodel/failures/onground_any` | On-ground status |
| `sim/flightmodel/position/vh_ind_fpm` | Vertical speed (FPM) |

## 🤝 Related Projects

This X-Plane client is part of the larger Virtual Flight Online Transmitter ecosystem:

- **Windows Client (MSFS)**: SimConnect-based transmitter for Microsoft Flight Simulator
- **Server (PHP/APCu)**: Web server with radar display, IVAO feeds, and JSON APIs
- **Web Radar**: Interactive Leaflet-based radar with multiple map layers and features

For the complete system including server setup, visit the main [Virtual Flight Online Transmitter](https://github.com/jonbeckett/virtualflightonlinetransmitter) repository.

## 📚 Support & Resources

| Resource | Link |
|----------|------|
| **FlyWithLua Forum** | [X-Plane.org Forums](https://forums.x-plane.org/index.php?/forums/forum/314-flywithlua/) |
| **X-Plane Support** | [X-Plane.org](https://www.x-plane.org/) |
| **Main Transmitter Project** | [GitHub Repository](https://github.com/jonbeckett/virtualflightonlinetransmitter) |

## 📄 License

This script is licensed under **GPL-3.0**. See the main project repository for full license details.

## 📜 Version History

### Version 1.3 (Current)
- Improved connection timeout handling (200ms for minimal blocking)
- Non-blocking send operations for better performance
- Enhanced error logging with reconnection status
- Auto-connect and hide at startup feature

### Version 1.2
- Persistent HTTP connections with keep-alive
- Automatic reconnection on connection drop
- Improved error handling and logging

### Version 1.1
- Added ImGui-based user interface
- Persistent configuration storage
- Text-to-speech feedback for connection status

### Version 1.0
- Initial release
- Real-time position transmission using LuaSocket
- Basic configuration options
- Landing detection with touchdown velocity tracking
- Cross-platform support (Windows, macOS, Linux)

---

**Last Updated:** December 2025  
**Current Version:** 1.3
