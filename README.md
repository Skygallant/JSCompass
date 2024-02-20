This is a watch face I made using watch face format. It works like Jack Sparrow's compass from the Pirates of the Caribbean movies.

# Things I Used for Building:
To build the watch face I used a .sh script I found here: https://github.com/android/wear-os-samples/blob/main/WatchFaceFormat/build-wff.sh
It's fairly straightforward, you just need to set up some environment stuff and throw in the files from this repo.
The watch face can't do much on its own though, apart from telling the time, so you'll need the two companion complication services I wrote to accompany it.
they can be found here: https://github.com/Skygallant/JSCompassRose and here: https://github.com/Skygallant/JSCompassDestiny
The Compass Rose app should build fine in Android Studio, but the Compass Destiny will need a Google Maps API key which can be generated here: https://console.cloud.google.com/google/maps-apis/credentials
put your API key into your local.properties file and call it like so: `GOOGLE_MAPS_API_KEY=xxxxxxxxxx`
then the app should work.

# How to Install:
You'll need a WearOS device that supports: compass, GPS, network, and accelerometer readings. Oh, and the watch face is made for 450x450 resolution displays, but it might work on others? I'm not sure how watch face format handles that.
Load up the 2 companion complication apps first, the watch face will initialise them when it loads, so they need to be ready. They both need Location and Notification Permissions and these must be set through your device's settings menu.
Because I was not able to figure out how to make the pop-up appear since the complication services don't have activities. Once the two complication companion apps are ready you can load up the watch face and everything should JustWork™

# How to Use:
The two complications can be updated by tapping on the upper/lower halves of the screen. the upper half will update the destiny compass and the lower half will update the compass rose.
the "Compass Rose" is what I call the red N/S/E/W compass, which orients north, and even accounts for magnetic declination
the "Destiny Compass" is the gold star in the middle (you can't miss it!) and it is the *star* of the show!
It will point to a random location within walking distance of where you first tapped the screen, and when you get to that location, the watch should vibrate and it'll pick a new place to explore automagically! It's the perfect companion for your adventures.

# Troubleshooting:
There are a few toast messages the app uses to alert the user to problems, there is "Rose Perms" if the compass rose companion has not had its permissions set, and there is "Rose Pos" if the compass rose can not find a GPS signal, and similar functionality for the destiny compass with "Compass Pos" and "Compass Perms".
Something else to keep in mind is if you tap the top of the watch to update the destiny compass, and there is no current location seelcted to point to, you will get a "Fate" toast. This means that the watch is busy selecting a location. After a couple of seconds, you can tap again to update the compass normally.
Also, there is currently a debug toast message that tells you the name of the location that the Destiny Compass is pointing to. This isn't really how it's supposed to work, it's supposed to be a surprise, but until I am comfortable that the geofencing is working, I'll leave it in.
