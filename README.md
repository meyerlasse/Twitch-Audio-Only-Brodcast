# Twitch Audio-Only Restreamer

This script takes a Twitch.tv username and restreams the audio on a local Icecast2 server, while the stream is online.
Every 60 seconds, the availability of the Twitch stream is checked and the audio stream started accordingly.
The mountpoint of the audio stream on Icecast is the Twitch username.

Example:
Twitch username: restreamer --> URL: localhost:8000/restreamer

Can be easily modified to be usable for other streaming sites as well.

## Dependencies

- [youtube-dl](https://rg3.github.io/youtube-dl/): Downloading the stream
- [ffmpeg](https://ffmpeg.org/): Converting the stream to MP3 and provide a source for the Icecast2 server
- [icecast2](http://icecast.org/): Making the audio stream available on the network

## Setup

1. Install the required packages:
   ```bash
   sudo apt-get install youtube-dl ffmpeg icecast2
   ````

2. Configure Icecast2

3. (Optional) Configure systemd service file `twitch-audio-restream.service`
	- Add Twitch username
	- Add Icecast source password

4. (Optional) Install systemd service file
   ```
   sudo cp twitch-audio-restream.service /etc/systemd/system
   sudo systemctl enable twitch-audio-restream.service
   ```

5. (Optional) Copy script to location where systemd service file expects it
   ```
   sudo mkdir -p /opt/twitch-audio-restream
   sudo cp twitch-audio-restream.sh /opt/twitch-audio-restream/
   ```

6. Start either script directly or systemd service

   `./twitch-audio-restream.sh [Twitch username] [icecast source password]`

   or

   `sudo service twitch-audio-restream start`

