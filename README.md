# obs2zoom

obs2zoom is a script to configure [PulseAudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) and its Acoustic Echo Cancellation (AEC) features for use with [OBS Studio](https://obsproject.com) (OBS).  obs2zoom should very loosely mimic the functionality of [Virtual Audio Cable](https://vb-audio.com/Cable/) to route your audio from your Microphone, to OBS, to your preferred video conferencing application like [Zoom](https://zoom.us), [Google Meet](https://meet.google.com), [Google Duo](https://duo.google.com), [WebEx](https://www.webex.com), [BlueJeans](https://www.bluejeans.com), and more.

obs2zoom allows you to configure and deconfigure PulseAudio as needed for use with OBS without the need to set "permanent" configurations in /etc/pulse/default.pa or ~/.config/pulse/default.pa.


# Usage

To run obs2zoom and configure PulseAudio devices

    obs2zoom start

To stop obs2zoom and remove the created virtual devices

    obs2zoom stop

In OBS, go to File->Settings->Audio->Advanced, and select 'Monitor of OBS monitor sink'.

![image](https://user-images.githubusercontent.com/12750133/111318703-4d1afb00-8633-11eb-9d89-5c1c7e3aa78d.png)


Next, create a scene, and add the following sources:

- Audio Input Capture (pulseaudio): Name it 'Echo Cancelled Microphone', and select the device with the same name.
- Audio Input Capture (pulseaudio): Name it 'Microphone', and select the physical microphone that you will use for input.
- Audio Output Capture (pulseaudio): Name it 'To OBS', and select the device with the same name.
- Audio Output Capture (pulseaudio): Name it 'To OBS (Monitored)', and select the device with the same name.

![image](https://user-images.githubusercontent.com/12750133/111318762-57d59000-8633-11eb-84cb-d0668b1fef87.png)


Now go to Edit->Advanced Audio Properties, and set the Audio Monitoring like so:

- Echo Cancelled Microphone - Monitor Off
- Microphone - Monitor Only (mute output)
- To OBS - Monitor Off
- To OBS - Monitor and Output

![image](https://user-images.githubusercontent.com/12750133/111318798-602dcb00-8633-11eb-9a76-864081ee619e.png)


Now all the hard stuff is done. Open whatever VidConf software you are using, and select:

- Microphone -> 'Echo Cancelled Microphone'
- Speakers -> 'Echo Cancelled Speakers'

![image](https://user-images.githubusercontent.com/12750133/111318854-6fad1400-8633-11eb-9249-03e5bc40633c.png)


obs2zoom has been tested on Zoom (duh), Webex, Google Meet, Google Duo, MS Teams, BlueJeans, and Signal Desktop.

# Filters

If you would like to add filters (like Noise Suppression, or Noise Gate) to your capture device, add them to 'Microphone'.

![image](https://user-images.githubusercontent.com/12750133/114203366-b71a7d80-991d-11eb-83dc-c47b40699585.png)


# Credit

obs2zoom was written with tips and suggestions from these links:

- [PulseAudio Documentation](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/)

- [Arch Linux Wiki](https://wiki.archlinux.org/index.php/PulseAudio/Examples)

- [OBS Project Forum](https://obsproject.com/forum/threads/virtual-audio-cable-for-zoom.125072/#post-503142)


# Additional resources

To use obs2zoom with [OBS v26.1.0](https://github.com/obsproject/obs-studio/releases/tag/26.1.0) or greater utilizing its built-in Virtual Camera functionality, install v4l2loopback.

- https://github.com/umlaeute/v4l2loopback
