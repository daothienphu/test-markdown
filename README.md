# **MEPInstant documentation**  
## Version 2.9.8  
## Last updated: 2021/12/03  

# **Table of contents:**

## 1. Functions
- [createCustomHapticFeedback](#createcustomhapticfeedback)
- [createHapticFeedback](#createhapticfeedback)
- [createMusicPlayer](#createmusicplayer)
- [emitCustomEvent](#emitcustomevent)
- [endGame](#endgame)
- [firstStart](#firststart)
- [getAsyncPlaylist](#getasyncplaylist)
- [getAsyncSongContent](#getasyncsongcontent)
- [getComponent](#getcomponent)
- [getDefaultOrSetConfidenceSetting](#getdefaultorsetconfidencesetting)
- [getDefaultOrSetOnSetCombineSettings](#getdefaultorsetonsetcombinesettings)
- [getGameDataAsync](#getgamedataasync)
- [getNotesAsync](#getnotesasync)
- [getPlatform](#getplatform)
- [getPlayerID](#getplayerid)
- [getSDKVersion](#getsdkversion)
- [getSpecificContent](#getspecificcontent)
- [hidePlatformLoadingScreen](#hideplatformloadingscreen)
- [initializeAsync](#initializeasync)
- [isPvP](#ispvp)
- [loadDynamicScript](#loaddynamicscript)
- [onDisconnect](#ondisconnect)
- [onGameResult](#ongameresult)
- [onPause](#onpause)
- [onResume](#onresume)
- [onStartCountDown](#onstartcountdown)
- [onStartPvP](#onstartpvp)
- [playPredefinedHaptic](#playpredefinedhaptic)
- [readNotebotv4AsMIDI](#readnotebotv4asmidi)
- [sendCountDownRequest](#sendcountdownrequest)
- [sendDataRequest](#senddatarequest)
- [sendGameEndLoop](#sendgameendloop)
- [sendGameReady](#sendgameready)
- [sendHeartRequest](#sendheartrequest)
- [sendScoreRequest](#sendscorerequest)
- [setGameDataAsync](#setgamedataasync)
- [SetNoteBotV4Settings](#setnotebotv4settings)
- [showReviveConfirmation](#showreviveconfirmation)
- [SongRewardAdsClick](#songrewardadsclick)
- [startGame](#startGame)
- [startGameAsync](#startgameasync)

## 2. Classes
- HowlerAudio
- SuperpoweredAudio
- MusicPlayer
- NoteBotConverter
- LevelReader
- LevelBotGenerator

## 3. Enumerations
- [GameMode](#gamemode)
- [HapticMode](#hapticmode)

## 4. Objects
- [GameData](#gamedata)
- [GameData.Song](#gamedatasong)
- [GameData.Configs](#gamedataconfigs)
- [GameData.SpecificContent](#gamedataspecificcontent)
- [GameData.Player](#gamedataplayer)
- [GameResult](#gameresult)
- [MIDI](#midi)
- [MIDI.NoteMIDI](#midinotemidi)
- [NoteBotV4Settings](#notebotv4settings)
- [NoteBotV4Settings.ConfidenceSettings](#notebotv4settingsconfidencesettings)
- [NoteBotV4Settings.OnsetCombineSettings](#notebotv4settingsonsetcombinesettings)
- [SongListData](#songlistdata)


## 5. Typical Game Flow
- [Initialization](#initialization)
- Music and Level Controller
- PvP

# ***1.Functions (Top level namespace: MEPInstant)***
# **initializeAsync()** 
## &nbsp;&nbsp; **Description:**  
- Initializes the SDK, downloads the levelReader and the levelBotGenerator scripts. They are the essential scripts for level creation and generation. **initializeAsync** should be called before any other method.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.initializeAsync()
```
## &nbsp;&nbsp; **Paremeters:**  
- none  
## &nbsp;&nbsp; **Return value:**  
- **Promise\<void\>**: resolves if the scripts are downloaded successfully.  
## &nbsp;&nbsp; **Examples:**
```js
MEPInstant.initializeAsync().then(function() {
  // Many properties will be null until the initialization completes.
  // This is a good place to fetch them:
  var platform = MEPInstant.getPlatform(); // 'IOS'
  var sdkVersion = MEPInstant.getSDKVersion(); // '2.0'
  var playerID = MEPInstant.getPlayerID();
});
```


# **startGameAsync()**
## &nbsp;&nbsp; **Description:**  
- Starts the game flow. 
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.startGameAsync()
```
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **Promise\<[GameData](#gamedata)\>**: resolves with the [GameData](#gamedata) object.  
## &nbsp;&nbsp; **Examples:**
```js
MEPInstant.startGameAsync().then(gameData => this.setupGame(gameData));
```


# **getSpecificContent()**
## &nbsp;&nbsp; **Description:**  
- Gets the [SpecificContent](#gamedataspecificcontent) array.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getSpecificContent()
```
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **Array\<[SpecificContent](#gamedataspecificcontent)\>**: the specific content array.
## &nbsp;&nbsp; **Examples:**
```js
let specificContent = MEPInstant.getSpecificContent();
let fileType1 = specificContent[0].fileType;
```


# **createMusicPlayer()**
## &nbsp;&nbsp; **Description:**  
- Creates an instance of the MusicPlayer class.
## &nbsp;&nbsp; **Syntax:**  
```js
createMusicPlayer(src, onLoad) //for SuperpoweredAudio
createMusicPlayer(src, loop, onLoad, onPlay, onEnd) //for HowlerAudio
```
## &nbsp;&nbsp; **Paremeters:**  
- `src:` **string** URL of the mp3 music file.  
- `loop:` **boolean** true if the audio should play on loop.
- `onLoad:` **Function** Called after the audio is loaded.  
- `onPlay:` **Function** Called when the audio is played.  
- `onEnd:` **Function** Called after the audio has stopped.
## &nbsp;&nbsp; **Return value:**  
- **MusicPlayer** The MusicPlayer instance.  
## &nbsp;&nbsp; **Examples:**
```js

```

# **getNotesAsync()**
## &nbsp;&nbsp; **Description:**  
- Gets the [MIDI](#midi) data of the song.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getNotesAsync(levelUrl)  
MEPInstant.getNotesAsync(levelUrl, isDefaultFilter) //for manual content  
MEPInstant.getNotesAsync(levelUrl, noteBotV4Settings) //for noteBotv4  
```  
## &nbsp;&nbsp; **Paremeters:**  
- `levelUrl:` **string** URL to the level file. Currently, the only supported manual content file types are .bin, .mid, .encrypt, or .encrypted.  
- `isDefaultFilter:` **boolean**  
- `noteBotV4Settings:` **[NoteBotV4Settings](#notebotv4settings)** settings for the note bot v4.  
## &nbsp;&nbsp; **Return value:**  
- `[MIDI](#midi)` The MIDI data of the song.
## &nbsp;&nbsp; **Examples:**
```js

```


# **onPause()**
## &nbsp;&nbsp; **Description:**  
- Pauses the game but does *not* pause the MusicPlayer instance.  
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onPause(callback)
```
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after pausing the game.  
## &nbsp;&nbsp; **Return value:**  
- void  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onPause(() => {
  console.log('Pause Game');
});
```


# **onResume()**
## &nbsp;&nbsp; **Description:**  
- Shows the "Tap to play" screen then calls the callback function. If the game is in PvP mode, only calls the callback function.   
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onResume(callback)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after resuming the game.  
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onPause(() => {
  console.log('Resume Game');
});
```


# **isPvP()**
## &nbsp;&nbsp; **Description:**  
- Checks whether the game is in PvP mode.  
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.isPvP()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none  
## &nbsp;&nbsp; **Return value:**  
- **boolean**: true if the game is in PvP mode, false otherwise. 
## &nbsp;&nbsp; **Examples:**  
```js
if (MEPInstant.isPvP()) {
  self.isTutorial = false;
}
```


# **sendGameReady()**
## &nbsp;&nbsp; **Description:**  
- Sends the game ready signal to the other players in the same lobby. Only for PvP mode.  
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendGameReady()
```   
## &nbsp;&nbsp; **Paremeters:**  
- none  
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
if (this.player.ready) {
  MEPInstant.sendGameReady();
}
```


# **onStartCountDown()**
## &nbsp;&nbsp; **Description:**  
- Starts the countdown on the screen and calls the callback function. Only for PvP mode.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onStartCountDown(callback)
```    
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after starting the countdown.  
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onStartCountDown(() => {
  console.log("countdown started");
}
```


# **onStartPvP()**
## &nbsp;&nbsp; **Description:**  
- Starts the game and calls the callback function. Only for PvP mode.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onStartPvP()
```
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after starting the game.  
## &nbsp;&nbsp; **Return value:**  
- void  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onStartPvP(() => {
  this.startRound();
})
```


# **onGameResult()**
## &nbsp;&nbsp; **Description:**  
- Calls the callback function when the game ends. Only for PvP mode.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onGameResult(callback)
```
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after the game ends.  
## &nbsp;&nbsp; **Return value:**  
- void  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onGameResult(() => this.EndGame());
```


# **onDisconnect()**
## &nbsp;&nbsp; **Description:**  
- Forces to end the game. Only for PvP mode.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.onDisconnect(callback)
```
## &nbsp;&nbsp; **Paremeters:**  
- `callback:` Function Called after the player disconnected.  
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.onDisconnect(() => this.EndGame());
```


# **createHapticFeedback()**
## &nbsp;&nbsp; **Description:**  
- Creates a haptic feedback based on one of the predefined haptic modes.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.createHapticFeedback(hapticType)
```
## &nbsp;&nbsp; **Paremeters:**  
- hapticType: **number** The type of haptic feedback. See [HapticMode](#hapticmode).
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.createHapticFeedback(MEPInstant.HapticMode.lightImpact);
MEPInstant.createHapticFeedback(0);
```


# **createCustomHapticFeedback()**
## &nbsp;&nbsp; **Description:**  
- Creates a customized haptic feedback.
## &nbsp;&nbsp; **Syntax:**  
```js
createCustomHapticFeedback(intensity, sharpness, duration, isContinuous)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `intensity:` **number** The intensity of the haptic feedback.  
- `sharpness:` **number** The sharpness of the haptic feedback.  
- `duration:` **number** The duration of the haptic feedback.  
- `isContinuous:` **boolean** true if the haptic feedback is continuous, false otherwise.
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.createCustomHapticFeedback(0.65, 0.1, 0.2, true);
```


# **sendDataRequest()**
## &nbsp;&nbsp; **Description:**  
- Sends a request to update a data value.  
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendDataRequest(dataObject);
```
## &nbsp;&nbsp; **Paremeters:**  
- dataObject: 
## &nbsp;&nbsp; **Return value:**  
- void  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.sendDataRequest({score: this.score});
```


# **getSDKVersion()**
## &nbsp;&nbsp; **Description:**  
- Gets the current SDK version.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getSDKVersion();
```
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **string**: the current version of the SDK.
## &nbsp;&nbsp; **Examples:**  
```js
var sdkVersion = MEPInstant.getSDKVersion(); // '2.9.8'
```


# **sendHeartRequest()**
## &nbsp;&nbsp; **Description:**  
- Sends a request to update the *heart* value
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendHeartRequest(value);
```
## &nbsp;&nbsp; **Paremeters:**  
- value: **number** The new value of *heart*.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
if (MEPInstant.hasOwnProperty('sendHeartRequest')) {
  MEPInstant.sendHeartRequest(this.numMissAccept);
}
```


# **showReviveConfirmation()**
## &nbsp;&nbsp; **Description:**  
- Shows a binary choice on screen for the user to confirm or cancel the revival. Once the choice has been made, sends the game results to the server for further processing and analysis.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.showReviveConfirmation(onYesCallback, onNoCallback, gameResult)
```
## &nbsp;&nbsp; **Paremeters:**  
- `onYesCallback:` **Function** Called when the user confirms the revival.  
- `onNoCallback:` **Function** Called when the user cancels the revival.  
- `gameResult:` **[GameResult](#gameresult)** The game results to be sent.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.showReviveConfirmation(
  () => {
    this.reviveRound();
  },
  () => {
    this.EndGame();
  },
  this.result
)
```


# **endGame()**
## &nbsp;&nbsp; **Description:**  
- Sends the end game signal and sends the [GameResult](#gameresult) to the server.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.endGame(result)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `result:` **[GameResult](#gameresult)** The game results to be sent. 
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.endGame(this.result)
```


# **startGame()**
## &nbsp;&nbsp; **Description:**  
- Starts the game.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.startGame(result)
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **void**  
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.startGame()
```


# **SetNoteBotV4Settings()**
## &nbsp;&nbsp; **Description:**  
- Sets the settings for the NoteBotV4.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.SetNoteBotV4Settings(confidence, onsetCombine)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `confidence:` **[ConfidenceSettings](#notebotv4settingsconfidencesettings)** The confidence settings.
- `onsetCombine:` **[OnsetCombineSettings](#notebotv4settingsonsetcombinesettings)** The on set combine settings.
## &nbsp;&nbsp; **Return value:**  
- **[NoteBotV4Settings](#notebotv4settings)**: The settings for the NoteBotV4.
## &nbsp;&nbsp; **Examples:**  
```js

```


# **SongRewardAdsClick()**
## &nbsp;&nbsp; **Description:**  
- Shows rewards 
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.SongRewardAdsClick(onSuccess, onFailure)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `onSuccess:` **Function** Called when the player successfully watched the ad.
- `onFailure:` **Function** Called when the player failed to watch the ad.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js

```


# **emitCustomEvent()**
## &nbsp;&nbsp; **Description:**  
- Invokes a custom event.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.emitCustomEvent(eventName, payload)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `eventName:` **string** The name of the event.
- `payload:` **object** The payload of the event, depends on the event.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
var data = {
  id: platform.gameData.player.id
};
MEPInstant.emitCustomEvent('gameReady', {data: data});
```


# **firstStart()**
## &nbsp;&nbsp; **Description:**  
- Initiates the MEPUtilities and BundleManager instances.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.firstStart()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.firstStart()
```


# **getAsyncPlaylist()**
## &nbsp;&nbsp; **Description:**  
- Gets the playlist from a URL.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getAsyncPlaylist(url, maxSongCount, offset)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `url:` **string** The URL of the playlist.
- `maxSongCount:` **number** the maximum number of songs to be returned.
- `offset:` **number** the offset of the start of the playlist.
## &nbsp;&nbsp; **Return value:**  
- **Array\<[SongListData](#songlistdata)\>:** The song playlist.
## &nbsp;&nbsp; **Examples:**  
```js

```


# **getComponent()**
## &nbsp;&nbsp; **Description:**  
- Gets the LevelReader instance or the LevelBotGenerator instance.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getComponent(name)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `name:` **string** The name of the component, either LevelReader or LevelBotGenerator.
## &nbsp;&nbsp; **Return value:**  
- **LevelReader** or **LevelBotGenerator**: an instance of either LevelReader of LevelBotGenerator class.
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.getComponent(LevelReader)
```


# **getAsyncSongContent()**
## &nbsp;&nbsp; **Description:**  
- Gets the song content from a URL
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getAsyncSongContent(url, songName)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `url:` **string** The URL of the playlist.
- `songName:` **string** The name of the song.
## &nbsp;&nbsp; **Return value:**  
- 
## &nbsp;&nbsp; **Examples:**  
```js

```


# **sendScoreRequest()**
## &nbsp;&nbsp; **Description:**  
- Sends a request to update the score of the player.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendScoreRequest(value)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `value:` **number** The new score value.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.sendScoreRequest(69)
```


# **sendCountDownRequest()**
## &nbsp;&nbsp; **Description:**  
- Sends a request to show the countdown.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendCountDownRequest()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.sendCountDownRequest()
```


# **getPlatform()**
## &nbsp;&nbsp; **Description:**  
- Gets the current playform
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getPlatform()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **string:** The current platform.
## &nbsp;&nbsp; **Examples:**  
```js
let platform = MEPInstant.getPlatform()
```


# **getPlayerId()**
## &nbsp;&nbsp; **Description:**  
- Gets the player's ID.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getPlayerId()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **string:** The player's ID.
## &nbsp;&nbsp; **Examples:**  
```js
let playerID = MEPInstant.getPlayerId()
```


# **setGameDataAsync()**
## &nbsp;&nbsp; **Description:**  
- Sets the game data of the player.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.setGameDataAsync(data)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `data:` **[GameData](#gamedata)** The game data of the player.
## &nbsp;&nbsp; **Return value:**  
- **Promise\<void\>** resolves if the player data has been updated successfully.
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.setGameDataAsync(this.gameData);
```


# **getDefaultOrSetConfidenceSetting()**
## &nbsp;&nbsp; **Description:**  
- Gets the default [ConfidenceSettings](#notebotv4settingsconfidencesettings) or sets the new [ConfidenceSettings](#notebotv4settingsconfidencesettings) with the given variables.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getDefaultOrSetConfidenceSetting(vocalMin, melodyMin, drumMin)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `vocalMin:` **number**
- `melodyMin:` **number**
- `drumMin:` **number**
## &nbsp;&nbsp; **Return value:**  
- **[ConfidenceSettings](#notebotv4settingsconfidencesettings)** The confidence settings.
## &nbsp;&nbsp; **Examples:**  
```js
let confidenceSettings = MEPInstant.getDefaultOrSetConfidenceSetting(100, 100, 100);
```


# **getDefaultOrSetOnSetCombineSettings()**
## &nbsp;&nbsp; **Description:**  
- Gets the default [OnsetCombineSettings](#notebotv4settingsonsetcombinesettings) or sets the new [OnsetCombineSettings](#notebotv4settingsonsetcombinesettings) with the given variables.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getDefaultOrSetOnSetCombineSettings(
  minSilenceTimeToConsiderMerging, 
  minTimeDistanceToHighPriorityNoteAfterMerge, 
  maxHighPriorityNoteDuration, 
  isAlsoCombineBeatTracking, 
  isSyncNotePowerWithBeatPower, 
  minValidBeatPowerDB)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `minSilenceTimeToConsiderMerging:` **number**
- `minTimeDistanceToHighPriorityNoteAfterMerge:` **number**
- `maxHighPriorityNoteDuration:` **number**
- `isAlsoCombineBeatTracking:` **boolean**
- `isSyncNotePowerWithBeatPower:` **boolean**
- `minValidBeatPowerDB:` **number**
## &nbsp;&nbsp; **Return value:**  
- **[OnsetCombineSettings](#notebotv4settingsonsetcombinesettings)** The on set combine v4 settings.
## &nbsp;&nbsp; **Examples:**  
```js
let onsetCombineSettings = MEPInstant.getDefaultOrSetOnSetCombineSettings(0.3, 0.3, 2, false, true, 52);
```


# **getGameDataAsync()**
## &nbsp;&nbsp; **Description:**  
- Gets the game data of the player.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.getGameDataAsync()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **Promise\<[GameData](#gamedata)\>** resolves with the [GameData](#gamedata) of the player.
## &nbsp;&nbsp; **Examples:**  
```js
let data = MEPInstant.getGameDataAsync();
```


# **hidePlatformLoadingScreen()**
## &nbsp;&nbsp; **Description:**  
- Hides the loading screen.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.hidePlatformLoadingScreen()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.hidePlatformLoadingScreen();
``` 


# **loadDynamicScript()**
## &nbsp;&nbsp; **Description:**  
- Downloads a script from a URL.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.loadDynamicScript(scriptUrl, onComplete)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `scriptUrl:` **string** The URL of the script.
- `onComplete:` **Function** The callback function to be called when the script is loaded.
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.loadDynamicScript();
```


# **playPredefinedHaptic()**
## &nbsp;&nbsp; **Description:**  
- Plays a predefined haptic.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.playPredefinedHaptic(pattern)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `pattern:`   
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.playPredefinedHaptic(pattern);
```


# **readNotebotv4AsMIDI()**
## &nbsp;&nbsp; **Description:**  
- Gets the MIDI data of a song from a URL.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.readNotebotv4AsMIDI(url, isEncrypt)
```  
## &nbsp;&nbsp; **Paremeters:**  
- `url:` **string** The URL of the song.
- `isEncrypt:` **boolean** true if the song is encrypted (fileType .encrypt, .encrypted).
## &nbsp;&nbsp; **Return value:**  
- **Promise\<[MIDI](#midi)\>** resolves with the MIDI data of the song.
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.readNotebotv4AsMIDI(url, isEncrypted);
```


# **sendGameEndLoop()**
## &nbsp;&nbsp; **Description:**  
- Sends a signal indicating that the game loop has ended.
## &nbsp;&nbsp; **Syntax:**  
```js
MEPInstant.sendGameEndLoop()
```  
## &nbsp;&nbsp; **Paremeters:**  
- none
## &nbsp;&nbsp; **Return value:**  
- **void**
## &nbsp;&nbsp; **Examples:**  
```js
MEPInstant.sendGameEndLoop();
```





# ***3.Enumerations***
# **HapticMode**
- 0: light impact
- 1: medium impact
- 2: heavy impact
- 3: success notification
- 4: warning notification
- 5: error notification
- 6: selection
  

# **GameMode**
- 0: normal mode
- 2: PvP mode


# ***4.Objects***
# **GameData**  
- `song:` **[Song](#gamedatasong)** The song data.  
- `configs:` **[Configs](#gamedataconfigs)** The game configurations.  
- `autoSpecificConetent:` **boolean** true if the specific content is automatically generated, false otherwise.  
- `specificContent:` **[SpecificContent](#gamedataspecificcontent)** The specific content data.  
- `player:` **[Player](#gamedataplayer)** The player data.  
- `gameMode:` **number** The current game mode. See **[GameMode](#gamemode)**    
- `isMultiMissEnable:` **boolean** true if the player can miss the first few notes, false otherwise.  
- `numMissAccept:` **number** The number of times the player can miss before losing.  


# **GameData.Song**  
- `id:` **string** The song's ID.  
- `title:` **string** The song's title.  
- `artist:` **string** The song's artist.  
- `duration:` **number** The song's duration.  
- `mp3Url:` **string** The song's URL.  
- `levelUrl:` **string** The level's URL.  


# **GameData.Configs**
- `isUseSuperpowered:` **boolean** true if the MusicPlayer initilized the song as SuperpoweredAudio, false otherwise.  
- `isEndlessMode:` **boolean** true if the game is in endless mode, false otherwise.    
- `isDebug:` **boolean** true if the game is in debug mode, false otherwise.  
- `isAutoPlay:` **boolean** true if the game is in auto play mode, false otherwise.  
- `loop:` **number** The number of loops.  


# **GameData.SpecificContent**  
- `contentUrl:` **string** The specific content's URL.  
- `fileType:` **string** The specific content's file type.  


# **GameData.Player**  
- `id:` **string** The player's ID.  
- `name:` **string** The player's name.  
- `avatarUrl:` **string** The player's avatar URL.  

# **GameResult**
- `score:` **number** The player's score.
- `star:` **number** The amount of stars the player has earned.
- `crown:` **number** The amount of crowns the player has earned.
- `notes:` **number** The amount of notes the player has hit.
- `stage:` **number**  
- `loop:` **number** The amount of loops that the player is on.
- `continue_count:` **number** The amount of revivals the player has done.
- `song_percent:` **number** The percentage of the song that has been played.
- `fps_95:` **number**  
- `fps_drop_count:` **number**  
- `fps_drop_events:` **number**  

# **NoteBotV4Settings**
- `confidenceSettings:` **[ConfidenceSettings](#notebotv4settingsconfidencesettings)**
- `onsetCombineSettings:` **[OnsetCombineSettings](#notebotv4settingsonsetcombinesettings)**

# **NoteBotV4Settings.ConfidenceSettings**
- `vocalConfidenceMin:` **number**
- `melodyConfidenceMin:` **number**
- `drumConfidenceMin:` **number**

# **NoteBotV4Settings.OnsetCombineSettings**
- `MinSilenceTimeToConsiderMerging:` **number**
- `MinTimeDistanceToHighPriorityNoteAfterMerge:` **number**
- `MaxHighPriorityNoteDuration:` **number**
- `IsAlsoCombineBeatTracking:` **boolean**
- `IsSyncNotePowerWithBeatPower:` **boolean**
- `MinValidBeatPowerDB:` **number**

# **SongListData**
- `songID:` **string** The song's ID.
- `songName:` **string** The song's name.
- `artistName:` **string** The song's artist.
- `thumbnailUrl:` **string** The song's thumbnail URL.
- `unlockType:` 

# **MIDI**
- `notes:` **Array<[NoteMIDI](#midinotemidi)>**
- `fullnotes:` **Array<[NoteMIDI](#midinotemidi)>**
- `notesLineIndex:` **Array<number>** The lines of each notes.
- `duration:` **number** The duration of the song.
- `bpm:` **number** the BPM of the song.
- `ppq:` **number** the PPQ of the song.
- `difficulties:` 
- `applySanityCheck():` **Function**
- `selectNotesByLines():` **Function**
- `filterByEnergyLevel():` **Function**

# **MIDI.NoteMIDI**
- `midi:` **number** The MIDI value.
- `name:` **string** The note's name.
- `time:` **number** The note's starting time.
- `ticks:` **number** The pulse at which the note starts.
- `duration:` **number** The note's duration.
- `durationTicks:` **number** The amount of ticks the note lasts. 



# ***Typical Game Flow***
# **Initialization**
The initialization process for every game must start with [initializeAsync()](#initializeasync) followed by [startGameAsync()](#startgameasync), [onPause()](#onpause), and [onResume()](#onresume).
```js
initializeSDK(): 
{
  MEPInstant.initializeAsync().then(() => 
  {
    MEPInstant.startGameAsync().then(gameData => this.start(gameData));
    MEPInstant.onPause(() => {
      console.log('paused');
      this.pause();
    })
    MEPInstant.onResume(() => {
      console.log('resumed');
      this.resume();
    })
  })
}
```


questions:  
what is isDefaultFilter  
dataobject in senddatarequest  
gameresult?  
profilermanager?    
dancing road doesnt set the game state to start game  
startgame vs startgameasync vs firstStart?   
haptic pattern in playPredefinedHaptic  
notes and fullnotes in MIDI  
  
