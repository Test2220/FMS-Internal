---
description: >-
  This page will describe the Web-Socket and the methods to update the client
  and how it relates to the point system and the external controls.
---

# Cheesy Arena Web-socket

Most of Cheesy Arena dynamic content are encoded into a web-socket json packet. Notable locations are the Field Testing Panel, Match Play Panel, Field monitor, Audience display, and other dynamic content panels.  Each section will describe what packets are receive and can be sent to Cheesy Arena.

## General information

The way that Cheesy arena formats their packet is in a Type field and a Data field which its the payload for that specific data type.  This is also the same for sending data to Cheesy Arena. From here onward the Headers will Denote packet types&#x20;

```json
{"type": [Data Packet Type],"data":[payload]}
```

### Ping

The Ping Packet confirms that the client is still receiving data from the web-socket server, no response is needed however to keep the connection alive&#x20;

```json
{"type":"ping","data":null}

```

### arenaStatus

The Arena State Packet is one of the basic packet that gets sent from Cheesy Arena and will be seen the most in logging.  In the Json it will contain the entire arena state from the driver station and teams and what mode Cheesy Arena is in. A Sample Packet is below.  Notably the driver station is abbreviated so use the key below to indicate what driver station should be disabled.  This relationship does follow through in other data packets as well.

| Drive Station | Payload key |
| ------------- | ----------- |
| Blue 1        | B1          |
| Blue 2        | B2          |
| Blue 3        | B3          |
| Red 1         | R1          |
| Red 2         | R2          |
| Red 3         | R3          |

#### Match State

The match state key is denotes what mode the FMS is in from the driver station.  Use the table below to see what state is what.

<table><thead><tr><th width="92" data-type="number">Value</th><th width="146">Arena State</th><th>Description </th></tr></thead><tbody><tr><td>0</td><td>PreMatch</td><td>Field not running human and robots are allowed on the field</td></tr><tr><td>1</td><td>StartMatch</td><td>FMS starting the match</td></tr><tr><td>2</td><td>WarmupPeriod</td><td>Any precode that needs to run before match runs gets executed here</td></tr><tr><td>3</td><td>AutoPeriod</td><td>Robots are in Auto Mode</td></tr><tr><td>4</td><td>PausePeriod</td><td>The time period between Auto and Teleop</td></tr><tr><td>5</td><td>TeleopPeriod</td><td>Robots are in Teleop mode</td></tr><tr><td>6</td><td>PostMatch</td><td>Match is complete final edits to score can be made this is where the FMS team can signal in Volunteers and reset</td></tr><tr><td>7</td><td>TimeoutActive</td><td>Time out timer is running</td></tr><tr><td>8</td><td>PostTimeout</td><td>Timeout Timer is completed</td></tr></tbody></table>



{% code overflow="wrap" %}
```json
{
  "type": "arenaStatus",
  "data": {
    "MatchId": 0,
    "AllianceStations": {
      "B1": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      },
      "B2": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      },
      "B3": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      },
      "R1": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      },
      "R2": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      },
      "R3": {
        "DsConn": null,
        "Ethernet": false,
        "Astop": false,
        "Estop": false,
        "Bypass": false,
        "Team": null
      }
    },
    "TeamWifiStatuses": {
      "B1": {
        "TeamId": 0,
        "RadioLinked": false
      },
      "B2": {
        "TeamId": 0,
        "RadioLinked": false
      },
      "B3": {
        "TeamId": 0,
        "RadioLinked": false
      },
      "R1": {
        "TeamId": 0,
        "RadioLinked": false
      },
      "R2": {
        "TeamId": 0,
        "RadioLinked": false
      },
      "R3": {
        "TeamId": 0,
        "RadioLinked": false
      }
    },
    "MatchState": 0,
    "CanStartMatch": false,
    "PlcIsHealthy": false,
    "FieldEstop": false,
    "PlcArmorBlockStatuses": {
      "BlueDs": false,
      "RedDs": false
    }
  }
}
```
{% endcode %}

### ToggleBypass

Toggle bypass turns on the bypass for the specific driver station.  This command can only be sent from the Match Play screen.&#x20;

```
{"type":"toggleBypass","data":"B1"}
```

### updateRealtimeScore

This updates the the score in 6 sections divided up by the Blue alliance and the Red Alliance in each major section in a match Auto, Teleop, and Endgame.  For the update to work you have to send the whole data packet, you cannot send just the updated section, the whole state needs to be updated all at once.

```json
{"type":"updateRealtimeScore",
"data":{
    "blueAuto":0,
    "redAuto":0,
    "blueTeleop":0,
    "redTeleop":0,
    "blueEndgame":0,
    "redEndgame":0
    }
}
```
