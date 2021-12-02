# **MEPInstant documentation**  
## Version 2.9.7  
## Last Updated: 2021/12/03  

# **Table of contents:**


## Functions
### [initializeAsync ](#initializeasync)
### [onPause ](#onpause)


## Classes
### HowlerAudio
### SuperpoweredAudio
### MusicPlayer


## Enumerations


## Objects
### [GameData ](#gamedata)
### [GameData.Song ](#gamedatasong)
### [GameData.Configs ](#gamedataconfigs)
### [GameData.SpecificContent ](#gamedataspecificcontent)
### [GameData.Player ](#gamedataplayer)


## Typical Game Flow


# Functions (Top level namespace: MEPInstant)
## **initializeAsync** 
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; Initializes the SDK, downloads the levelReader and the levelBotGenerator scripts. They are the essential scripts for level creation and generation. **initializeAsync** should be called before any other method.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```MEPInstant.initializeAsync()```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; ***Promise\<void\>***: resolves with the downloaded *levelReader* and the *levelBotGenerator* scripts.  
### &nbsp;&nbsp; **Examples:**
```
MEPInstant.initializeAsync().then(function() {
  // Many properties will be null until the initialization completes.
  // This is a good place to fetch them:
  var platform = MEPInstant.getPlatform(); // 'IOS'
  var sdkVersion = MEPInstant.getSDKVersion(); // '2.0'
  var playerID = MEPInstant.getPlayerID();
});
```


## **startGameAsync**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; Starts the game flow. 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```startGameAsync()```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; **Promise\<void\>**: resolves with the [GameData ](#gamedata) object.  
### &nbsp;&nbsp; **Examples:**
```
MEPInstant.startGameAsync().then(gameData => this.setupGame(gameData));
```


## **getSpecificContent**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; Gets the [SpecificContent ](#gamedataspecificcontent) array.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```getSpecificContent()```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; ***Array\<[object](#gamedataspecificcontent)\>***: the specific content array.
### &nbsp;&nbsp; **Examples:**
```
let specificContent = MEPInstant.getSpecificContent();
let fileType1 = specificContent[0].fileType;
```


## **createMusicPlayer**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function to create an instance of the MusicPlayer singleton class.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```createMusicPlayer(src, onLoad) //for SuperpoweredAudio```  
&nbsp;&nbsp;&nbsp;&nbsp; ```createMusicPlayer(src, loop, onLoad, onPlay, onEnd) //for HowlerAudio```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; src: url of the mp3 music file.  
&nbsp;&nbsp;&nbsp;&nbsp; loop: 
&nbsp;&nbsp;&nbsp;&nbsp; onLoad: load successful callback function.  
&nbsp;&nbsp;&nbsp;&nbsp; onPlay: callback function.  
&nbsp;&nbsp;&nbsp;&nbsp; onEnd: callback function.
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; a MusicPlayer instance.


## **getNotesAsync**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that returns an object containing the note layout and relevant information of the level.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```getNotesAsync(levelUrl)```  
&nbsp;&nbsp;&nbsp;&nbsp; ```getNotesAsync(levelUrl, isDefaultFilter)```  
&nbsp;&nbsp;&nbsp;&nbsp; ```getNotesAsync(levelUrl, isDefaultFilter, noteBotV4Settings)```  
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```levelUrl:``` **string** URL to the level file. Currently, the only supported manual content file types are .bin, .mid, .encrypt, or .encrypted.
&nbsp;&nbsp;&nbsp;&nbsp; ```isDefaultFilter:``` **boolean**  
&nbsp;&nbsp;&nbsp;&nbsp; ```noteBotV4Settings:``` **object** settings for the note bot v4.  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; an object containing the following properties: notes, fullNotes, notesLineIndex, duration, bpm, ppq, difficulties; and the following methods: applySanityCheck, selectNotesByLines, filterByEnergyLevel.


## **onPause**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that pauses the game (but does not pause the MusicPlayer instance).  
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```onPause(callback)```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; callback: a callback function.  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void  


## **onResume**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that shows the "Tap to play" screen then calls the callback function. If the game is in PvP mode, it will only call the callback function.   
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```onResume(callback)```  
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; callback: a callback function.  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void  


## **isPvP**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that returns whether the game is in PvP mode or not.  
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```isPvP()```  
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; ***bool***: true if the game is in PvP mode, false otherwise. 


## **sendGameReady**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function specifically designed for PvP mode, it sends the game ready signal to the other players in the same lobby.  
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```sendGameReady()```   
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void  


## **onStartCountDown**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function specifically designed for PvP mode, it starts the countdown screen and calls the callback function.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```onStartCountDown(callback)```    
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; callback: a callback function.
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void


## **onStartPvP**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function specifically designed for PvP mode, it starts the game and calls the callback function.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```onStartPvP()```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; callback: a callback function.
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void


## **onGameResult**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 


## **onDisconnect**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 


## **createHapticFeedback**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 


## **createCustomHapticFeedback**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```createCustomHapticFeedback(intensity, sharpness, duration, isContinuous)```  
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; intensity: a float value indicating the intensity of the haptic feedback.  
&nbsp;&nbsp;&nbsp;&nbsp; sharpness: a float value indicating the sharpness of the haptic feedback.  
&nbsp;&nbsp;&nbsp;&nbsp; duration: a float value indicating the duration of the haptic feedback.  
&nbsp;&nbsp;&nbsp;&nbsp; isContinuous: a bool value to show whether the haptic is continuous.  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void  


## **hasOwnProperty**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Examples:** 


## **sendDataRequest**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 


## **getSDKVersion**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; Gets the current SDK version.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```MEPInstant.getSDKVersion()```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; ***string***: the version of the SDK.
### &nbsp;&nbsp; **Examples:**  
```
var sdkVersion = MEPInstant.getSDKVersion(); // '2.9.8'
```


## **sendHeartRequest**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ``````
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; 
### &nbsp;&nbsp; **Examples:**  
&nbsp;&nbsp;&nbsp;&nbsp; 


## **showReviveConfirmation**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that prompts a binary choice on screen for the user to confirm or cancel the revival. Once the choice has been made, the game will send back the game results to the server for further processing.
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```showReviveConfirmation(onYesCallback, onNoCallback, gameResult)```
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; onYesCallback: a callback function that will be called when the user confirms the revival.  
&nbsp;&nbsp;&nbsp;&nbsp; onNoCallback: a callback function that will be called when the user cancels the revival.  
&nbsp;&nbsp;&nbsp;&nbsp; gameResult: an object that contains the game results, including the following fields: score, star, crown, percent, loop, notes, revise. 
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void


## **endGame**
### &nbsp;&nbsp; **Description:**  
&nbsp;&nbsp;&nbsp;&nbsp; a function that sends the ending signal to the game.  
### &nbsp;&nbsp; **Syntax:**  
&nbsp;&nbsp;&nbsp;&nbsp; ```endGame()```  
### &nbsp;&nbsp; **Paremeters:**  
&nbsp;&nbsp;&nbsp;&nbsp; none  
### &nbsp;&nbsp; **Return value:**  
&nbsp;&nbsp;&nbsp;&nbsp; void  

# **Game flow documentation**
First, we need to initialize the game using **initializeAsync()**. Then, 
**startGameAsync()**, **startGameAsync()** will call the necessary functions to download the game data. After which, we need to use **getSpecificContent()** to get those data. **createMusicPlayer()** -> **getNotesAsync()**

# **Objects**


## **GameData**  
### ```song:``` **object** The song data.  
### ```configs:``` **object** The game configurations.  
### ```autoSpecificConetent:``` **boolean** true if the specific content is automatically generated, false otherwise.  
### ```specificContent:``` **object** The specific content data.  
### ```player:``` **object** The player data.  
### ```gameMode:``` **enum** The current game mode {0: normal mode, 2: PvP mode}.  
### ```isMultiMissEnable:``` **boolean** true if the player can miss the first few notes, false otherwise.  
### ```numMissAccept:``` **number** The number of times the player can miss before losing.  


## **GameData.Song**  
### ```id:``` **string** The song's ID.  
### ```title:``` **string** The song's title.  
### ```artist:``` **string** The song's artist.  
### ```duration:``` **number** The song's duration.  
### ```mp3Url:``` **string** The song's URL.  
### ```levelUrl:``` **string** The level's URL.  


## **GameData.Configs**
### ```isUseSuperpowered:``` **boolean** true if the MusicPlayer initilized the song as SuperpoweredAudio, false otherwise.  
### ```isEndlessMode:``` **boolean** true if the game is in endless mode, false otherwise.    
### ```isDebug:```  **boolean** true if the game is in debug mode, false otherwise.  
### ```isAutoPlay:```  **boolean** true if the game is in auto play mode, false otherwise.  
### ```loop:```  **number** The number of loops.  


## **GameData.SpecificContent**  
### ```contentUrl:``` **string** The specific content's URL.  
### ```fileType:``` **string** The specific content's file type.  


## **GameData.Player**  
### ```id:``` **string** The player's ID.  
### ```name:``` **string** The player's name.  
### ```avatarUrl:``` **string** The player's avatar URL.  


question:
what is isDefaultFilter


redo:
create music player
