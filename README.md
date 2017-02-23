RepoFiles
======
A repository used for easy management of files used by other repos.

Note: You should be using a Windows platform with a C: drive if you want to properly use this repo. You can try using it on other
platforms, but the whole point of this is to keep everyone's file references the same so that we don't have clashing when we push and pull each other's changes. **If you can't use the C: drive**(low space, don't want files there, etc), you could try making a **junction** and have the repo files actually **reside elsewhere on your computer**, but still be accessible from C:\Java.
**To make a junction**, follow the steps below. (If you know how to already, you can skip this.)

 - Hold down shift and right click on the C:\ root drive folder, then select "Open command window here". Command prompt should open.
(You may need to open cmd prompt as an administrator, then type "cd/d C:\" if you encounter access denied errors or similar.)
- Type "mklink /J Java PATHHERE" where PATHHERE is the full path to the actual Java folder that you are keeping elsewhere.
- Verify success by going to C:\Java and checking the repo files. If C:\Java doesn't have the same file contents as the root of this repository, it won't work. To remove the junction link and try again, type "rd Java" in the same cmd prompt window whose working directory(cd) is still C:\\. DON'T use the explorer window to delete the junction! You may end up deleting the linked folder as well!

Bug Reporting
-------------
There's actually not any code in this repo(except the buildtools files, but those don't count),
but if there's a file related issue, go right ahead and report it!

Repository Setup
-----------------
The main folder for this repo is C:\Java. all the files in this repo should go directly into that folder. For example, the full
path to the bukkit .jar that you'd use on a bukkit or spigot repo's build path should be:
C:\Java\Libraries\Minecraft\BuildTools\1.11.2\Bukkit\target\bukkit-1.11.2-R0.1-SNAPSHOT.jar
(If the BuildTools folder proves too much to be able to download when you download the project files, try only downloading the
BuildTools.jar and then just running buildtools in the C:\Java\Libraries\Minecraft\BuildTools\1.11.2\ folder, again ensuring that
the full paths of the files contained within match the repo's, then just download the rest of the repo files if not already.)

There are also some other directories to note:

 - C:\Java\Libraries\Minecraft\ -> Eclipse project build path .jars(libraries) go here.
	Ex. worldedit-bukkit-6.1.4-SNAPSHOT-dist.jar or Vault.jar
- C:\Java\jres -> This folder contains java installations for your eclipse projects to use instead of whatever Java you have installed on your pc. That way, if you update Java on your pc, your workspace settings and build path will remain unaffected.
	The one you'll probably use most is C:\Java\jres\jre1.8.0_91. Should that need to be updated that to the latest Java version, it's ok to update it, but let everyone using this repo know before you do so that they can prepare their workspace settings in Eclipse. Also, try to include the src.zip file located at [jrefolder]\lib\src.zip. If you don't know where to get this file, let me ([Brian_Entei](https://github.com/br45entei)) know the jre or jdk version and I'll download the src.zip and add it to the repo. Thanks!
- C:\Java\Eclipse_Settings -> This folder contains settings that you'll need your Eclipse IDE to be using.
		- There are presently three files of interest in this folder:
			- **java_syntax.epf** -> This file contains both of the profiles listed below as well as all other required Eclipse settings, as well as a custom syntax coloring theme for coding that I created myself.
			- "**Java code style clean up profile.xml**" and "**Java code style formatter profile.xml**" -> These are the exported profiles for the Compiler clean-up and formatter, used by Eclipse whenever you finish editing a file and click save.
				- Clean-up can be used by going to **Source -> Clean up** in Eclipse with the class file in question open, then following the dialog instructions. Clean-up will organize and move your class's methods around and sort them alphabetically and list static methods and fields in the top of the file. If you don't want this to happen, don't worry, it won't happen normally when you just click save. You have to manually use clean-up. I'd recommend saving clean-up for when you have a messy file that you've obtained elsewhere, and need to make heads or tails out of it.
				- Formatter is used by Eclipse automagically whenever you save a java class file after editing. It organizes the imports, cleans up the coding style(placement of brackets, parenthesis, tabs and spaces, excessive empty/blank lines...) but is not too strict on what it formats so as to keep your sanity intact. If it does not appear to be working whenever you save, you'll need to change the following setting in Eclipse or just re-import the java_syntax.epf file to fix it: Navigate to **Window -> Preferences** then on the left, go to **Java -> Editor -> Save Actions**. Now make sure "**Perform the selected actions on save**" is checked and then make sure that all of the remaining check boxes are saved. As for the radio option, I'd recommend selecting "**Format all lines**". Now click 'Apply' then 'Ok' and the changes should take effect immediately, but you may need to restart Eclipse if it still doesn't seem to format your source code when you re-edit and save the file to check. If, after restarting, it *still* doesn't seem to work, check and make sure you actually imported the formatter profile, which is described below.
				- If you don't want to use my Java syntax coloring(black background with yellow, green and white text for easy readability), then don't import the ***java_syntax.epf*** file, but instead import the two xml profiles to their appropriate places in Eclipse's settings. To do this, first start with the "***Java code style clean up profile.xml***" file by going into Eclipse and doing **Window -> Preferences**, then go under **Java -> Code Style -> Clean Up** and click "**Import...**". Then navigate to the xml file and click open.
	For the next xml profile, keep the preferences window open from just now and go down to "**Formatter**" to the left.
	Now import the second xml file, just like before. Now you can click "Apply" then "Ok", and you'll likely need to restart Eclipse after this point in order to prevent 'strange things' from happening(Eclipse gets weird when you change a lot of settings all at once, it happens sometimes).
					- Please note that **if you don't import java_syntax.epf**, you won't be using the same error and warning settings that everyone else will(or at least should) be using for Eclipse[warnings such as boxing/unboxing, static access, qualified access, unused variable warnings, else clause warnings... things that help you keep the code clean, neat, and easy for everyone to read ;)]. This can result in confusion as to why some code raises errors or certain "**@SuppressWarnings("")**" tags or similar are used in one person's workspace, but apparently unneeded in another person's workspace.
A way **to get around this** and **use the settings from java_syntax.epf without using the color theme** would be to uncheck "**Import All**" when importing the epf file, then uncheck "**Java Appearance Preferences**" and make sure everything else is checked, and then you should have all settings except for the color theme.

Contributing
------------
This repo shouldn't be used to distribute code, rather the files behind the scenes used and needed by code in other repositories. If you are contributing to a repository that uses this one for build path files, and you need to add a library .jar or other files, let everyone know ahead of time before you commit so that we can be sure we really need the file. Once done, everyone will need to pull the changes down to their Eclipse workspaces and update all of their repositories that are using this one. This includes settings in Eclipse such as build path, java jre installations, and even eclipse preference settings and xml profiles. Once all build paths are fixed/updated and settings re-imported as needed, a quick restart of Eclipse should remedy any remaining errors, unless a required build path file was removed from this repo accidentally, in which case we'll need to get one person to reverse the latest commit and restore the missing files. Hopefully that won't happen, though! Happy coding! :)
