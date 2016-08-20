MapVote
=======================

MapVote is a wonderful little GMOD13 addon originally made by [Willox](http://steamcommunity.com/id/Willox303) that allows you to easily invoke a map vote from within any gamemode of your choosing.

This version forks Tyrantelf's version.

The following changes were made:
* Modified to include all maps with the prefix(es) located in the 'gamemode'.txt file by default. This allows it to work on ideally all gamemodes.
* Allows you to include more maps for a specific gamemode

Installation
======================
* If applicable, unsubscribe to any previous MapVote addons and remove it from the collection that the server uses
* Download and just drag the lua folder into steamcmd\steamapps\common\GarrysModDS\garrysmod. **This will overwrite any existing files related to MapVote if you had any previously.** This is important only if you made any custom changes to the sourcode previously.


Usage
=======================

Starting a vote from within lua is rather simple.

```Lua
MapVote.Start(voteLength, allowCurrentMap, mapLimit, mapPrefix)
```
All arguments to this function are optional and the map prefix is acquired from gamemode.txt file, if available, otherwise, uses the ones from the config file.
You can also set up defaults within garrysmod/data/mapvote/config.txt which is generated during the first run.

It is also possible to cancel map votes from within lua with:
```Lua
MapVote.Cancel()
```

You can give players extra voting power in lua/autorun/mapvote.lua with the MapVote.HasExtraVotePower function, and a config will be added at some point.

TTT and Deathrun Setup
=======================

You no longer have to edit any files for MapVote to work with Trouble in Terrorist Town or Deathrun anymore! It now overrides the default functions for map switching.

*Note: On Deathrun, it still uses the build in RTV, so changing the minimum player count doesn't work*

You can edit the config.txt located in garrysmod/data/mapvote/ to change several settings. It should look like this by default (if it's empty, just copy this into it):
```JSON
{
	"RTVPlayerCount": 3,
	"AdditionalMaps": 
	{
		"murder": "gm_housewithgardenv2|de_forest|cs_office|cs_italy"
	},
	"MapLimit": 24,
	"TimeLimit": 28,
	"AllowCurrentMap": false,
	"MapPrefixes": [],
	"MapsBeforeRevote": 3,
	"EnableCooldown": true
}
```
* "RTVPlayerCount" is the minimum number of players that need to be online (on TTT) for RTV to work.
* "AdditionalMaps" are the additional maps or map prefixes it should include for a specific gamemode.
* "MapLimit" is the number of maps shown on the vote screen.
* "TimeLimit" is how long the vote is shown for.
* "AllowCurrentMap" true/false to allow a the current map in the map vote list.
* "MapPrefixes" are the prefixes of the maps that should be used in the vote. **Leave it empty if you want to use the map prefixes found in the 'gamemode'.txt file.**
* "MapsBeforeRevote" is the number of maps that must be played before a map is in the vote menu again (if EnableCooldown is true)
* "EnableCooldown" is a true/false variable on whether to remove a map from voting for a while after it's played.
* "MapsBeforeRevote" is how many maps before the map is taken off the cooldown list after it's played.

To add more Map Prefixes, do this: 
```JSON
{
	"RTVPlayerCount": 3,
	"AdditionalMaps": 
	{
		"murder": "gm_housewithgardenv2|de_forest|cs_office|cs_italy"
	},
	"MapLimit": 24,
	"TimeLimit": 28,
	"AllowCurrentMap": false,
	"MapPrefixes": 
	[
		"ttt_",
		"zm_",
		"de_"
	],
	"MapsBeforeRevote": 3,
	"EnableCooldown": true
}
```

To add additional maps to specific gamemodes, do this: 
```JSON
{
	"RTVPlayerCount": 3,
	"AdditionalMaps": 
	{
		"murder": "gm_housewithgardenv2|de_forest|cs_office|cs_italy",
		"terrortown": "cs_"
	},
	"MapLimit": 24,
	"TimeLimit": 28,
	"AllowCurrentMap": false,
	"MapPrefixes": 
	[
		"ttt_",
		"zm_",
		"de_"
	],
	"MapsBeforeRevote": 3,
	"EnableCooldown": true
}
```
