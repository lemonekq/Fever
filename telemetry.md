# Guide and Endpoints for Lunar Client
<p align="center">Lunar Client API Documentation</p>

# Launcher

## https://servermappings.lunarclientcdn.com/ (R2)

## https://launcherupdates.lunarclientcdn.com (R2)

## https://api.modrinth.com/v2

## https://api.lunarclientprod.com/modrinth/v2 (CF/W D1)
`/project/<>/version?loaders=<fabric>&game_versions=<>`

`/projects?ids=<>`

## Playwire Rewards
> TODO
```
promotionId: se.id,
completed: 1
```

# Analitycs
<p align="center">Decided to make an seperate category for this, for now its an spyware :3</p>

## https://analytics.lunarclientprod.com/launcher/event
### Launcher Start (/launcher.start)
```
{
    "cpu_architecture": "",
    "cpu_brand": "",
    "cpu_cores": 0,
    "cpu_manufacturer": "",
    "cpu_physical_cores": 0,
    "cpu_vendor": "",
    "device_pixel_ratio": 1,
    "graphics": [
        {
            "model": "",
            "sub_vendor": "",
            "vendor": "",
            "vram": 0
        }
    ],
    "hardware_acceleration": true,
    "installation_id": "",
    "launcher_version": "",
    "machine_has_battery": false,
    "machine_is_vm": false,
    "machine_manufacturer": "",
    "machine_model": "",
    "machine_uptime": 2,
    "machine_version": "",
    "memory_swap_total": 0,
    "memory_total": 0,
    "monitors": [
        {
            "is_main": true,
            "model": "",
            "refresh_rate": 0,
            "resolution_height": 0,
            "resolution_width": 0,
            "vendor": ""
        }
    ],
    "operating_system": "",
    "operating_system_release": "",
    "player_uuid": "",
    "session_id": "",
    "silent": false
}
```
### Successful Launch (/launch.success) (ClientSide?)
```
{
    "cache_generated": false,
    "installation_id": "",
    "launch_id": "",
    "player_uuid": "",
    "statuses": [
        {
            "status": "PREINIT",
            "time_ms": 0
        },
        {
            "status": "INIT",
            "time_ms": 0
        },
        {
            "status": "STARTED",
            "time_ms": 0
        }
    ],
    "time_ms_to_jvm": 0
}
```
### Cancelled Launch (/launch.cancel)
> `launch_id` - Profile UUID
```
{
    "installation_id": "",
    "launch_id": "",
    "player_uuid": "",
    "status_cancelled": "",
    "status_elapsed_time": 0
}
```
### Init Launch (/launch.init)
```
{
    "cpu_architecture": "x64",
    "initiator": "home-launch-button",
    "installation_id": "",
    "launch_id": "",
    "operating_system": "",
    "operating_system_release": "",
    "player_uuid": "",
    "session_id": "",
    "settings_info": {
        "after_launch_action": "HIDE",
        "allocated_memory": 0,
        "is_default_launch_directory": true,
        "launch_directory": "/home/0x80/.minecraft",
        "resolution": {
            "fullscreen": false,
            "height": 480,
            "width": 854
        }
    },
    "version_info": {
        "branch": "master",
        "modpack": {
            "id": "",
            "modrinth": {
                "id": ""
            },
            "name": "Example Modpack"
        },
        "module": "fabric",
        "version": "1.20.4"
    }
}
```
### Modpack install
```
profile_id: id,
profile_name: name,
profile_modrinth_id: projectId,
profile_modrinth_name: title,
profile_modrinth_version_id: versionId,
profile_modrinth_version_name: name,
profile_game_version: gameVersion
```
### Version Change (version.switch)
```
{
    "from_version": {
        "branch": "master",
        "modpack": {
            "id": "",
            "modrinth": {
                "id": ""
            },
            "name": "Example Modpack"
        },
        "module": "fabric",
        "version": "1.20.4"
    },
    "installation_id": "",
    "player_uuid": "",
    "session_id": "",
    "to_version": {
        "branch": "master",
        "module": "fabric",
        "version": "1.20.4"
    }
}
```
### Route Change (route.switch)
> `/versions/lunar` or `/versions/modpacks`
```
{
    "attempting_to_focus": false,
    "initiator": "unknown",
    "installation_id": "",
    "player_uuid": "",
    "session_id": "",
    "value": "/versions/lunar",
    "window_id": "main"
}
```
### Set game branch (experimental, etc)
```
no data about this.
```
### Notification interaction (/notafication.interaction)
```
{
    "bypass_dnd": true,
    "installation_id": "",
    "interaction_type": "",
    "notification_id": "",
    "notification_type": "",
    "placement": "native",
    "player_uuid": "",
    "session_id": ""
}
```
### Blogpost Interaction (/blogpost.interaction)
```
{
    "installation_id": "",
    "interaction_type": "hover",
    "new_indicator_visible": true,
    "player_uuid": "",
    "position": 1,
    "post_id": "",
    "session_id": ""
}
```
### Sidebar Interaction (/sidebar.interaction)
```
{
    "destination": "",
    "entry_id": "",
    "hidden": false,
    "installation_id": "",
    "interaction_type": "hover",
    "player_uuid": "",
    "position": 4,
    "session_id": ""
}
```
### Modrinth mod toggle
```
profile_id: id,
profile_name: name,
profile_modrinth_id: projectId,
profile_modrinth_version_id: versionId,
profile_game_version: gameVersion,
mod_type: modType,
mod_file_name: fileName,
position: position,
enabled: enable
```
### Modrinth mod install
```
profile_id: id,
profile_name: name,
profile_modrinth_id: projectId,
profile_modrinth_version_id: versionId,
profile_game_version: gameVersion,
mod_modrinth_id: project_id,
mod_modrinth_version_id: id,
mod_modrinth_version_name: name,
mod_file_name: ???,
position: position,
overriding_previous_mod: currentJarHash
```
### PostInstall
```
Not much data about this:
  - installation_id, that can be found in $PROFILE\.lunarclient\launcher-cache\installation-id,
  - player_uuid
```

<br>

### Successful Reponse
```
{
    "success": true
}
```

### BONUS: Electron dummy crashReporter
```
logger.log("Starting Electron crashReporter"), electron.crashReporter.start({
            companyName: "",
            ignoreSystemCrashHandler: 1,
            productName: electron.app.name || electron.app.getName(),
            submitURL: "https://f.a.k/e",
            uploadToServer: 0,
            compress: 1
        })
```
