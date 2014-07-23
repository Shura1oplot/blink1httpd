blink(1) http server daemon
===========================

Simple http server built using [bottle](http://bottlepy.org/) web framework.
It allows you to control [blink(1)](http://thingm.com/products/blink-1/) remotely using shell scripts (wget, curl), web browser, IFTTT callbacks or everything that can send http requests.
It requires [python3-blink1lib](https://github.com/Shura1oplot/python3-blink1lib/) to be installed.

Usage
-----

```
usage: blink1httpd [-h] [-v] [-H HOST] [-p PORT] [-f] [-P FILE] [-o FILE]
                   [-e FILE] [-d]

Blink(1) http server daemon v0.1.1

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -H HOST, --host HOST  HTTP server host (default: localhost)
  -p PORT, --port PORT  HTTP server port (default: 8060)
  -f, --foreground      do not detach from the shell
  -P FILE, --pid-file FILE
                        pid file path (default: /var/run/blink1httpd.pid, not
                        available in foreground mode)
  -o FILE, --stdout FILE
                        redirect stdout to file (not available in foreground
                        mode)
  -e FILE, --stderr FILE
                        redirect stderr to file (not available in foreground
                        mode)
  -d, --debug           enable debug messages
```

Supported pathes:
* `/blink1/devices`
* `/blink1/<name>/on?r=<red>&g=<green>&b=<blue>&fading=<fading>&led=<led>`
* `/blink1/<name>/off?fading=<fading>&led=<led>`
* `/blink1/<name>/blink?r=<red>&g=<green>&b=<blue>&fading=<fading>&delay=<delay>&count=<count>`
* `/blink1/<name>/play/<pattern>?count=<count>`
* `/blink1/<name>/stop`

Where:
* `<name>` - serial number or name from `devices.json`
* `<pattern>` - patterns sequence name from `patterns.json`
* `<red>`, `<green>`, `<blue>` - color value between 0 and 255
* `fading` - millisecs for color fading
* `led` - specify led to use (omit to use both)
* `delay` - millisecs between changing colors
* `count` - how many times device blinks or plays `<pattern>` (infinity if omitted)

All arguments are optional. For more information see [python3-blink1lib](https://github.com/Shura1oplot/python3-blink1lib/).

`devices.json` example:
```json
{
    "living_room": "2000212B",
    "hall": "20002253"
}
```

`patterns.json` example:
```json
{
    "blink_red_blue": [
        [255, 0,   0,   300],
        [255, 0,   0,   200],
        [0,   0,   0,   500],
        [0,   0,   0,   200],
        [0,   0,   255, 300],
        [0,   0,   255, 200],
        [0,   0,   0,   300],
        [0,   0,   0,   200]
    ]
}
```
