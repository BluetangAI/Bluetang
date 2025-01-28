## 2024.4.2

* FEATURE - Analytics client is now automatically initialized and in scope for a game agent  
* FIX - Analytics WAMP component now uses the analytics topic config key to determine redis key  
* FIX - Locking TensorFlow to appropriate version on Windows  

## 2023.2.1

* FIX - Use interpolation order 0 in frame transformation pipeline resize  
* FIX - Use offshoot selection kwarg when discovering to avoid running code of all plugins  
* FIX - Sprite identifier now rejects sprites that don’t have the same shape as the query sprite when using constellation of pixels  
* FIX - Mild attempt to shutdown frame grabber process on game agent exception  

## 2022.1.0

Exiting Beta! Changed the versioning scheme to YEAR.QUARTER.RELEASE

* IMPROVEMENT - Easier framework installation; only the core gets installed with `bluetang setup`; other modules with more involved installation steps can be set up later as needed!  
* IMPROVEMENT - Added a `bluetang update` command; headache-free framework updates  
* IMPROVEMENT - Added a `bluetang modules` command to check the installation status of optional modules  
* MAJOR FEATURE - Cross-platform gameplay recording with `bluetang record`; capture keyboard/mouse inputs alongside frame buffers, which are optionally put through a reward function; data is neatly packed in a single HDF5 file when done  
* FEATURE - A "force" kwarg can now be passed to input controller methods to ignore the game focus requirement  
* FEATURE - Context frame captures can now be scoped to game plugins' screen regions  
* FEATURE - GameFrame objects now have a timestamp representing the capture time with microsecond precision  
* FEATURE - GameFrame objects can now hold frame bytes (for PNG data) instead of a frame array  
* FEATURE - FrameGrabber get_frames no longer requires shape and dtype information  
* FEATURE - Added a mechanism to register custom reward functions in a GameAgent  
* TWEAK - No longer halving width & height in context frame capture; frame transformation pipeline should be used instead  
* TWEAK - Files generated from any frame capture operation are now named with the timestamp instead of a random UUID4  
* FIX - CNNInceptionV3Classifier can now also handle uint8 dtypes  
* INTERNAL - Reshape metadata and timestamp are now encoded alongside frame bytes, saving a ton of reshape preparation logic  
* INTERNAL - Added 'PNG' operator in frame transformation pipelines  
* INTERNAL / REFACTOR - Better OS abstractions to control platform-specific snippets  
* NOTEBOOK - Added a Jupyter Notebook to demonstrate common operations with the input recording HDF5 files  

## 2022.4.1

* FIX - InceptionV3 context classifier is now using the newer normalize function instead of the old scale_range one  
* REFACTOR / FIX - Added a mechanism to handle scancodes for extended keys in NativeWin32 input controller. Fixes arrow keys on Windows :)  
* FIX - Added a dtype kwarg to FrameGrabber get_frames. Necessary when using 'FLOAT' pipeline operator  

## 2021.3.2

* FEATURE - Added 'FLOAT' operator in frame transformation pipelines (needed for DQN)  
* FEATURE - Added 'SSIM' mode to sprite identifier  
* FIX - Sprite identifier score thresholds now work consistently with all offered modes  
* FIX - Resolved an issue with sprite identifier constellation of pixels mode and sprites with alpha channel  
* FIX - Added macOS command key to KeyboardKey enum and added a mapping for PyAutoGUI input controller backend  
* FIX - Linux window controller will now only consider visible windows when attempting to find game windows  
* FEATURE - Better range normalization in bluetang.cv: ability to pass in target domain  

## 2021.2.1

* FEATURE - Added frame transformation pipelines  
* FIX - DQN and DDQN fixes and Windows compatibility tweaks  

## 2021.1.0

* FIX - Emptied out __init__.py for bluetang.input_controllers (AKA win32api trying to import on Linux)  

## 2021.0.9

* MAJOR CHANGE - Added a KeyboardKey enum containing all valid keys that can be pressed on a standard keyboard; all InputController methods that accept keys now require KeyboardKey items  
* FEATURE - Added a fully-compliant native Windows input controller that uses the SendInput DLL function  
* FEATURE - Added 'move', 'click_down' & 'click_up' to the InputController protocol; implemented them in PYAUTOGUI & NATIVE_WIN32  
* FEATURE - Context classifier validation during training can now be skipped  
* FEATURE - Context classifier model checkpoints can now be autosaved  
* FEATURE - Locate() from the SpriteLocator can now use screen regions  
* FIX - Prevented an empty list from reaching a min() call in locate_string  

## 2021.0.8

* FIX - macOS frame reshape error should be resolved; including the top bar as part of the capture until someone can find a programmatic way to get the inner window size  
* FEATURE - Added a Web Browser GameLauncher for people who want to tackle web games  
* FIX - Added a default static seed to the training of the context classifier dataset split operation  

## 2021.0.7

* REFACTOR - InputController now pivots on a backend to allow extension; PyAutoGUI extracted to a backend (default)  
* FIX - No CUDA initialization unless it's actually needed  
* FEATURE - New `bluetang window_name` command to assist in finding the proper kwargs["window_name"] for Game plugins  
* FIX - Stopped initializing a VisualDebugger instance on every new GameFrameBuffer. Huge performance gain in frame consumption rate  

## 2021.0.6

* FIX - DarwinWindowController `is_window_focused` should use process title and not name  

## 2021.0.5

* FIX - Initial AppleScript to find focused windows was fine, but macOS users need to use process name and not window name  

## 2021.0.4

* FEATURE - Added resize_window to all WindowController classes  
* TWEAK - Base Game Agent GameFrameLimiter FPS to 30  

## 2021.0.3

* FEATURE - Retina display detection and handling on macOS  
* FIX - Most mouse events were missing the window geometry offsets  
* FIX - Replaced the AppleScript used to determine the focused window so the visible title bar name can be used in all cases  

## 2021.0.2

* FIX - Conda not found on Windows `bluetang setup`  
* FIX - Version-locked Cython to version 0.26.1 because Kivy doesn't build on 0.27  

## 2021.0.1

* Initial Beta Release  