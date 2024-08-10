# Elgato EyeTV for TV Linux-Guide

Info how to use older USB EyeTV TV Tuner stick in modern Linux machine.
<br>
<br>

Originally stick was sold as "Pocke-sized TV for your Mac or PC" although  it was usable in Linux but in early days required "configuration things to be done". Modern Linuxes (author used Mint 21.3) has builtin support in OS.

Author bought over 10 years old stick from garage sales and most found internet articles (for linux operations) were explaining compiling kernel drivers etc magic...

### CONNECTION TESTING

Connect antenna to stick and stick to computer via USB port.

Check that Linux recognizes the stick

     *dmesg | grep dvb*

This command should give something like this for ok recognization:


[  222.056575] dvb-usb: found a 'Elgato EyeTV DTT' in cold state, will try to load a firmware<br>
[  222.057337] dvb-usb: downloading firmware from file 'dvb-usb-dib0700-1.20.fw'<br>
[  222.638164] dvb-usb: found a 'Elgato EyeTV DTT' in warm state.<br>
[  222.638446] dvb-usb: will pass the complete MPEG2 transport stream to the software demuxer.<br>
[  222.639563] dvbdev: DVB: registering new adapter (Elgato EyeTV DTT)<br>
[  222.640162] dvbdev: dvb_create_media_entity: media entity 'dvb-demux' registered.<br>
[  222.900710] dvbdev: dvb_create_media_entity: media entity 'DiBcom 7000PC' registered.<br>
[  223.186654] dvb-usb: schedule remote query interval to 50 msecs.<br>
[  223.186661] dvb-usb: Elgato EyeTV DTT successfully initialized and connected.<br>
[  223.186872] usbcore: registered new interface driver dvb_usb_dib0700<br>


### TV APPS

Author tried two apps succesfully, there are other apps too , including Plex server (but it requires apparantly bought license)

## VLC

VLC requires "channel list" before operations.

Install the scanning tool : *sudo apt-get install w-scan*

Scan: *w_scan -c FI -X > ~/channels.conf 2> ~/w_scan_log.txt*             (FI is the country code)

*w_scan_log.txt* reveals if any channel were found actually (see below for possible antenna worries)


Start VLC, Select Media/Open file and select *channels.conf*. Now UI starts with "tv usage buttons"

VLC offers subtexts selection (if they are sent with broadcast) as well teletex. Recoding is also possible


## Kaffeine

Start program, select Television / Channels, do the channel scan (remember "save" channels using "Add filtered" button....)

Kaffeine offers program guide, hence you can program any wished recordings


### POSSIBLE PROBLEM AREAS

1) Try another USB port if everthing fails (stick is  not recognized). There might be "not enough power" phenomena in the USB port . In authors ThinkCentre, only one of the two front ports was ok to be used.

2) Stick is recognized but no channels found; try another antenna than the provided small one, or even better user also antenna amplifier. In author's case, provided antenna was ok in city environment, but in countryside bigger indoor antenna and signal amplifier were needed to get any channels to be found

3) Channels were found earlier and TV was ok to watch,but now nothing can be seen/found: Do hard reset (unplug and plug again). In author's case the stick goes "silent" now and then and hard reset fixes the situation

    Command pair for reloading:

    *sudo rmmod dvb_usb_dib0700*
    
    *sudo modprobe dvb_usb_dib0700*

    Succes can be checked form journal: *journalctl -xe | grep dvb*











