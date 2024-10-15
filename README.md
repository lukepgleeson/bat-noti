# Bat-Noti

## Intro
One of the quirks of using i3 is that there is a lot of functionality you'd expect from an operating system/tiling manager that it just leaves out. One such thing is an alert for a low battery. After shopping around a bit, I couldn't find one that exactly suited my needs and after my computer running out of battery for the 10th time while watching YouTube I decided to create my own. 

The main functionality I was missing was that my Lenovo T480 has 2 batteries and I wanted a separate notification for each one rather than one notification for both.

I also thought to use the LEDs under my keyboard to flash to add to the alert using the brightnessctl package.

I wanted to have a properties file to define the options.

If that appeals to you, feel free to checkout/tweak/contribute towards this script.

## Installation

This installation guide assumes you have i3, notify-send and brightnessctl installed and configured.

Checkout the project in a directory of your choosing. For example mine is in `~/.local/bin`

Add the following line to your i3 config file:

    exec <absolute/path/to/location/of/file/bat-noti> -p <absolute/path/to/location/of/file/properties>

For use of the flashing keyboard LEDs, the `$USER` will need to be added to the `input` group:

    sudo gpasswd -a $USER input

That should be it! Make sure that the paths are absolute i.e. no use of ~ for home directory.

## Configure

Below is each line in the properties file with the default value and a description of the effect. 
Properties do not need to be in order but all must be present.

1. BATTERY_ALERT_PERCENTAGE_THRESHOLD defines the battery percentage at which the alert will occur. When the battery goes below this percentage the error message will occur.
<!--end list-->

    BATTERY_ALERT_PERCENTAGE_THRESHOLD=20

2. KEYBOARD_LED_ALERT determines whether the LEDs on the backlight will flash on the occurrence of the alert. The LEDs will flash twice before returning to whatever state the LEDs had been in before the alert occurred.
<!--end list-->

        KEYBOARD_LED_ALERT=true

3. ABSOLUTE_PATH_TO_NOTIFY_ICON gives the path to the icon you wish to use for the notify-send icon. This can be pointed to the icon given in this repo or gives the option for the user to use their own icon.
<!--end list-->

        ABSOLUTE_PATH_TO_NOTIFY_ICON=/some/path

4. This script works by having a loop which tests the battery percentage and then sleeping for an amount of time. WATCHDOG_TIME is this amount of time in seconds. 
<!--end list-->

        WATCHDOG_TIME=30

## Issues/Improvements

1. If the laptop has received the alert, is put to sleep and plugged in to charge over the charge of the alert threshold, then removed from the charger before awakening again, the alert will not go off after reaching the threshold again.

2. More configuration needed for allowing 2 alerts

3. Only supports the case of 2 batteries currently

4. More error handling needed.

## License

[MIT](https://choosealicense.com/licenses/mit/)
