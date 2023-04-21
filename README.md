# KuopioScape

Interactable gallery application of Kuopio, which also includes multiple arcade-centric minigames.

Supports Windows platform with either keyboard & mouse or VR headset, and mobile touchscreen devices using Android.



### Game explanation
When game starts, player arrives atop of Puijon torni, from which they can navigate around the walking plaform to find buttons leading to the gallery or the arcade room.

In said gallery the player can start a slideshow of images, taken from different points of Kuopio, or visit some of those places through 360-images.

On the other hand in the arcade room, the player can find the following games:

**Pigeon shooter**, where the objective is to shoot as many birds as possible with the given ammo. Player has 15 bullets to use each round, though with imaginative thinking it's possible to gain more points than intended.

**Can shooter**, in which the player has to knock all cans off the table in order to win. To achieve this, the player will be given 5 bullets each attempt.

**Puzzle game**, where the objective is to complete the puzzle, shocker. Player can choose which 1 of 3 images to complete. Images are changeable mid-game.

Player can change settings, such as game volume, text size and player height in the settings UI, found inside the menu.



### Controls

Keyboard & mouse:

> Look around = Move mouse
> 
> Teleport = Mouse LeftClick
> 
> Interact with buttons = Mouse RightClick
> 
> Interact with menu and UI = Mouse RightClick
> 
> Shoot (during minigames) = Mouse RightClick
> 
> Move puzzle pieces (during puzzle game) = Mouse LeftClick
> 
> Open menu = Keyboard Esc_(Escape)_


VR:

> Teleport = Left controller Trigger
> 
> Interact with buttons = Right controller Grab
> 
> Interact with menu and UI = Left controller Trigger **OR** Right controller Grab + Trigger
> 
> Shoot (during minigames) = Right controller Trigger
> 
> Move puzzle pieces (during puzzle game) = Right controller Trigger (hold Grab to point out the piece)
> 
> Open menu = Either controller Joystick / Touchpad Press


Mobile (onscreen controls):

> Look around = Joystick (Lower left corner)
> 
> Teleport = Touch area on screen
>
> Interact with buttons = Touch button on screen
> 
> Interact with menu and UI = Touch element on screen
> 
> Shoot (during minigames) = Shoot button (Lower right corner)
> 
> Move puzzle pieces (during puzzle game) = Touch desired piece and then touch where to set the piece
> 
> Open menu = Menu button (Upper right corner)



### Game logic explained

When app starts up, AssetManager recognises which platform is in use, which other scripts use to perform appropriate actions for that platform (eg. doesn't open full screen menu for VR).

When player presses a button, MouseSelection makes a Raycast from the right hand (or middle of screen or touch position on screen, depending on platform) to the button to determine the distance and to get the button name, which is used to differentiate what each button does in a switch case. After button is pressed, it flashes green and during that flash, MouseSelection is rendered disabled by an if condition at the start of Update. After the delay, MouseSelection changes pressed button's color back. Button is pressed when the interact input button is **released** when pointing to a button. This causes a problem where if gun is pointed at a button, bullet launches when the input button is **pressed** (stopping the game) and the button is clicked again when the input button is released afterwards (starting the game again).

When starting pigeon or can game, the AssetManager.SwitchGame() method gets the right hand's child (current hand model), deletes it and replaces it with the gun model. Same but reverse happens when game ends. Game ends if bullets run out, bullet hits any button or player teleports from menu.

When entering a 360 image, MouseSelection saves player's current location before teleporting player inside the image and when exiting the image, returns player to the aforementioned saved location. If VR is enabled, also rescales player to 0.1 to prevent player from just walking out of the image, as the image balls are quite small.



# !Important!

### Developement notes

When running app in Unity Editor,

- Enable _Developer mode_ from AssetManager in inspector
 
- Disable other player controls if not in use (eg. if using Player_Mouse, disable Player\_Mobile and Player\_VR)
 
- To use VR in Developer mode, enable _is XR Present_ from AssetManager in inspector
 
- To simulate VR using keyboard, enable _XR Device Simulator_ GameObject under _Player\_VR_ GameObject, otherwise disable it


### Build notes

When building the app, enable all Player\_\* controls to avoid possible control errors.

Check that the _XR Device Simulator_ is disabled, otherwise VR won't work.

Also disable _Developer mode_ from AssetManager in inspector (If left enabled, app doesn't automatically detect and change platforms upon running).
