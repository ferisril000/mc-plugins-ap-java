# mc-plugins-ap-java

# Useful Links
[Spigot API Documentation](https://hub.spigotmc.org/javadocs/spigot/overview-summary.html)

[Paper Server Downloads](https://papermc.io/downloads)

[Spigot API Downloads](https://getbukkit.org/download/spigot)

# Installation Instructions
Note that these instructions are for Windows devices only. Minecraft servers cannot be run on macOS.

## Downloading the Main Repository
Download this entire repository by clicking on the green "Clone or Download" button and "Download ZIP".

![Download the Repository](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap01.png?raw=true)

 Once it downloads, right click on the zip file and click "Extract All". Extract it to somewhere you'll remember it, we'll be needing its files later.

## Installing Java SE 11
Visit the [Java SE Downloads Page](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase11-5116896.html).

![Download Java SE 11](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap02.png?raw=true)

Accept the License Agreement, and then download `jdk-11.02_windows-x64_bin.exe`

You may need to make an Oracle account to download it. I just used my student email.

Once it downloads, run the executable. Just click next through everything, there are no settings you need to change.

## Installing Eclipse

Visit the [Eclipse Downloads Page](https://www.eclipse.org/downloads/packages/).

![Download Eclipse](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap03.png?raw=true)

Download the latest Windows version of the "Eclipse IDE for Java Developers". The file should be called `eclipse-java-20##-##-R-win32-x86_64.zip`

Once it downloads, extract the zip file and move the `eclipse` folder somewhere you want it. This is a standalone application. I put mine on my desktop.

Run the `eclipse.exe` file inside of the folder. Just leave the workspace as the default. Once it boots to the welcome page, you can close the app.

## Installing Minecraft
Visit the [Minecraft Download Page](https://my.minecraft.net/en-us/download/),

Download and run `MinecraftInstaller.msi`. The default install settings are fine.

Once installed, run the launcher and sign in.

Currently, Minecraft version 1.14 is the latest version (just released!), but we want version 1.13.2.

To set this up, click the three bars at the top right and switch over to the Launch options tab. Click the plus and add another launch profile, and set the game version to release 1.13.2.

Give it a name, and click Save. Switch back over to the News tab, and click the up arrow next to the Play button, and select the new launch profile you added.

Click the Play button, and the game will perform a first-boot. You can close the game and launcher once you reach the title page.

## Installing Optifine (Optional)
Although this is an optional step, it is **highly recommended** because it will result in better client performance across all computers.

Visit the [Optifine Downloads Page](https://optifine.net/downloads).

![Download Optifine](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap04.png?raw=true)

Download the latest version of Optifine for Minecraft 1.13.2. Make sure you use the `(mirror)` button since it avoids the bit.ly ads. Your file should be called `OptiFine_1.13.2_HD_U_E#.jar`.

Chrome may ask you if you want to keep the file, if so, click "Keep".

Run the file, and click install.

This will set up another launch profile in the Minecraft launcher.

![Launch Profiles](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap05.png?raw=true)

Make sure that when you boot the game next time you use the Optifine launch profile.

## Setting up the Server
Navigate to the location where you downloaded this repository. Extract the `Startup Files.zip` file inside it to the location you want your server kept in.

Rename the folder it extracted to from `Startup Files` to `Minecraft Server` or whatever you want your server folder to be called.

Navigate into the `server` folder and run `start.bat`. This will open a console window, which is the server running. It will eventully stop with an error.

![Server Error](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/cap06.png?raw=true)

Like the error says, you haven't agreed to the EULA. Minimize (not close!) the console and there will be a `eula.txt` in the same directory where the `start.bat` file was.

To agree to the EULA, you just have to change `eula=false` on the last line of the text file to `eula=true`. Make sure you save the file.

Once you have agreed to the EULA, switch back over to the console window and type "y" to restart. The server is now running.

Launch minecraft, and click multiplayer on the title screen. Click direct connect, and type in `localhost` as the Server Address.

Once you join the server, switch over to the console and type `op yourusernamehere`. You can now execute any commands you want in-game, like `/gamemode creative`.

**Optional: Offline Server Mode**

If you find yourself being unable to connect to the server because you could not authenticate with minecraft.net (because it was blocked on school wi-fi, or because you aren't connected to a network), you can turn on offline mode in the server settings. 

Note that this only works if you have signed into your minecraft account in the launcher before.

Navigate to where the `start.bat` file is and find a file called `server.properties` within the directory. Open it and find the line toward the bottom that says `online-mode=true`. Change it to `online-mode=false` and save the file.

Switch over to the console and type `stop`. It will stop and then promp you to restart, so type "y". Once it has restarted, try connecting to it again.

Note: If you enable this mode, the server will identify your username as a new player, so you will have to re-op yourself. Your inventory will also reset.

# Setting up eclipse

Start eclipse. Uncheck `Show Welcome Screen` box and close the welcome window.

### Getting rid of extra windows

Close all windows except for the `Project Explorer` and `Navigator` windows, which I prefer to leave on the left side. If one of these windows is missing, go under `Window`>`Show View`> and select the missing one.

### Importing this repository's demo projects
Close eclipse and navigate to your eclipse workspace. This will likely be at `C:\Users\YourLoginAccount\eclipse-workspace\`. Copy the contents of this repository's `eclipse-workspace` folder to your `eclipse-workspace` folder.

### Placing your API jar in a convenient location (Optional)
If you are the administrator on your computer, you may want to place your `spigot-1.13.2.jar` file, which is required to export your plugins, in a convenient location. Head to your `C:\` directory and make a new folder called `Eclipse-APIs` and drop the `spigot-1.13.2.jar` file here.

By doing this, the demo plugins will work **out of the box** without any build path configuration.

# Creating projects

// TODO


# Useful Techniques
Making plugins all comes down to creativity, both in the function of the plugin and in the design of its code. This section gives templates of techniques to get what you want done quickly and efficiently.

## Event Handling
In order to handle events, you'll need to implement Listener in your class

```java
public class Main extends JavaPlugin implements Listener {
```

and register your events through Bukkit when the plugin enables.

```java
@Override
public void onEnable() {
	Bukkit.getPluginManager().registerEvents(this, this);
}
```


All event handler methods look something like this:

```java
@EventHandler
public void whateverYouWantToCallIt(EventObject e) {
```

The event object has all of the properties you might need to interact with the event.
Here's a very simple example from the `GrapplingHook` plugin which cancels fall damage as long as a player is grappling.

```java
@EventHandler
public void onDamage(EntityDamageEvent e) { //fall damage canceler for those playing
	if ((e.getEntity() instanceof Player)&&(e.getCause().equals(DamageCause.FALL))&&teamValue((Player)e.getEntity())!=0) {
		e.setCancelled(true);
	}
}
```

Notice that unlike a PlayerInteractEvent, this can trigger for any entity, so we check that `e.getEntity() instanceof Player` before casting it to the player type to make other checks. This also immediately rules out doing these extra checks for non-players.

## Delay and Looping

Minecraft runs at 20 ticks per second, and waits for your code to execute before proceeding to the next tick. This creates a problem if you happen to create an infinite loop. Instead, if you wish to create any events that take course over a period of time, such as a constant homing effect, you must use a loop with a delay.

### Delay Function
Queues the code within to be executed after a delay, then proceeds to the next lines of code.
```java
Bukkit.getScheduler().runTaskLater(this, new Runnable() {public void run() {
	//your code here
}},DELAY_IN_TICKS);
```
Though it appears simple, this code is more finicky than you would expect because Java. We're going to use this function for debugging to print the current world time in ticks.
```java
public String getTime() {
	return "["+Bukkit.getServer().getWorlds().get(0).getTime()+"] ";
}
```

### Simple use of the Delay Function

Using a for loop with increasing delay, you can make a simple timer from multiple delayed events scheduled in advance, but it's hard to do much with it. The `runTaskLater` method *schedules* the task to be run, then continues. That's why this for loop must schedule events for `i*20` delay. It loads all of the `*tick*` messages in advance. 

```java
//5 second countdown
Bukkit.broadcastMessage(getTime()+"Timer started!");
for (int i=1; i<=5; i++) {
	Bukkit.getScheduler().runTaskLater(this, new Runnable() {public void run() {
		Bukkit.broadcastMessage(getTime()+"*tick*");
	}},20*i); //x second * 20 ticks/second
}
Bukkit.broadcastMessage(getTime()+"Done!");
```
Here's the output:

![Countdown Results](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/delay01.png?raw=true)

Please note that you cannot use `i` inside the delayed calls since Java doesn't know whether or not `i` will have been garbage collected due to the method completing.

But, what if you have a loop that could take effect for an infinite amount of time? We'll hit a stack overflow error on `i` eventually.

Or what about an event that occurs after it finishes? What if we want an alarm noise on our timer? 

Or what about a while loop with an end condition? We can't check end conditions every tick because all the future ticks are scheduled instantly, so what do we do?

[Recursion Time](https://www.google.com/search?q=recursion)

### Recursive use of the Delay Function

Here's a full-fledged timer class example. Since we don't really want to have to initialize a timer object, we'll just make it an entirely static class. That means that in our main class we can just do `Timer.startTimer(5);` to use it.

```java
public class Timer() {

	public static void startTimer(int seconds) {
		Bukkit.broadcastMessage(getTime()+"Timer started!");
		timerloop(seconds,seconds);
	}
		
	private static String getTime() {
		return "["+Bukkit.getServer().getWorlds().get(0).getTime()+"] ";
	}

	private void timerloop(int s, int start) {
		if (s > 0) {
			Bukkit.broadcastMessage(getTime()+"*tick* ("+(start-s)+"s)");
			Bukkit.getScheduler().runTaskLater(this, new Runnable() {public void run() {
				timerloop(s-1,start); //recursive step
			}},20); //static delay of 1s between iterations
		} else { //exit condition
			Bukkit.broadcastMessage(getTime()+"*DING*");
		}
	}
}
```

Here's the output:

![Countdown Results](https://github.com/ferisril000/mc-plugins-ap-java/blob/images/delay02.png?raw=true)

Pretty clean right? We even can say how many seconds it has been and do a special message when the timer ends. We couldn't do that before with the for loop.

Notice that any static data (in this case the initial amount of starting seconds) must be carried through local variables alongside the dynamic data (in this case the remaining seconds).

You can find examples of this across all of the provided plugins, but most are too complex to explain concisely here.
