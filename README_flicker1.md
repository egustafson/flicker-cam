flicker1 Cam Set-Up Notes
=========================

1. Fresh Raspberry Pi OS install (Buster)
2. Update and Upgrade

3. Enable camera:  `sudo raspi-config` & reboot.
4. Verify camera:  `vcgencmd get_camera` both supported and detected
   =1

## Install UV4L - https://www.linux-projects.org/uv4l/

* https://www.linux-projects.org/uv4l/installation/

1. `curl https://www.linux-projects.org/listing/uv4l_repo/lpkey.asc | sudo apt-key add -`
2. Add the following to /etc/apt/sources.list.d/uv4l.list (use
   stretch, even though the release is buster):
   `deb https://www.linux-projects.org/listing/uv4l_repo/raspbian/stretch stretch main`
3. `sudo apt update`
4. `sudo apt install uv4l uv4l-raspicam`
5. `sudo apt install uv4l-raspicam-extras`  ## installs boot scripts
6. `sudo apt install uv4l-server`  ## installs the http server  (port: 8080)

## TODO: Investigate hand tuning uv4l and create custom systemd script.

Reasonable settings, thus far:
  *  1280x720, H.264, 10 fps
  *  single client streaming through http
  -> ~0.40 amps @ 5v power draw
  -> ~40% cpu idle
  -> 1Ghz clock (stay's at 99-100%)
  -> Temp ?? (at 55c it was still rising)

If the streaming client is disconnected:
  -> ~0.14 amps @ 5v
  -> 90% cpu idle
  -> 75-80% clock scale (750-800 Mhz)
  -> temp: ?? settled to 40c after ~5 min
