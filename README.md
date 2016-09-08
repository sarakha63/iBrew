# iBrew Brewing on the 7th day

[iKettle 2.0](http://smarter.am/ikettle) and [Smarter Coffee](http://smarter.am/coffee) Interface


## Introduction
iBrew is a (python) interface to iKettle 2.0 and Smarter Coffee devices. It includes a console, monitor, command line interface, web interface and rest api. You can also use it in your own code. iKettle 2.0 v19 and SmarterCoffee v20 tested at the moment. Please share any other discoveries you made! 

This means your machine is free! You can connect it yourself and do whatever you want with it. Like interface it with your favorite smarthome controller!

   Signed Me!

#### Versions
 * PHASE 1: [BRAINSTORMING] v0.0 Bean Grinder Pack 
 * PHASE 2: [PROTOTYPE]     v0.1 White Tealeaf Edition 
 * PHASE 3: [PROTOCOL]      v0.2 Tea Noire Sweet 
 * PHASE 4: [CONSOLE]       v0.3 Kettle Rattle 
 * PHASE 5: [WEB]           v0.4 Brewing on the 7th day 
 * PHASE 6: [PRERELEASE]    v0.5 Dumb Dump Limited Collector Edition (numbered, signed by author)
 * PHASE 7: [FINALCUT]      v1.0 Out of order!
 
#### Upcoming for the last 3 versions  
 * Timers protocol
 * Time arguments (have not figured that out)
 * Better error handling (sometimes it does not quit :-)
 * it also hangs if you scan wifi too much (luckily it reconnects, can not fix this)
 * Connecting in console mode... fails sometimes, and after reconnect is had strange data... stupid threads... missing...
 * Web interface & rest api (rest almost finished, uhum, web interface still have to create some pages) and introduce webroot & api key, login, license,...,...
 * History message is not finished
 * Fahrenheid not finished, please to not use.
 * v0.5 Missing Coffee Smarter codes (working bit only?)
 * fix wireless with the same name
 * watersensor to something usefull
 * Currently the default values in fast mode are not initalized use slow or give all values
 * filter out wrong responses... of know commands??? or atleast acknowledge them, (03 responses)
 * have not looked at single cup... needs a remote coffee machine session ;-)
 * strip zero from ip

#### Contact
[Bugs or issues](https://github.com/Tristan79/iBrew/issues). Donations & other questions <tristan@monkeycat.nl>
If you have jokes on coffee, tea, hot chocolade, coffee machines or kettles, please post in the issues.

Still no coffee machine (so no web for that)! I could like to thank Ju4ia for letting me access his coffee machine remotely, and get more Smarter Coffee missing protocol bits, and... that I could test the client code. And thanks for jkellerer for supplying coffee codes!


## Installation

#### Software Requirements 

* python 2.7
* python package: wireless
* python (optional) package: tornado 
* python (optional) package: pybonjour

#### Download
You can download and unpack the [source](https://github.com/Tristan79/iBrew/archive/master.zip) or download it from github using [Github Desktop](https://desktop.github.com) or manually:

```
git clone https://github.com/Tristan79/iBrew.git
```

#### Setup

Run ```make``` or ```pip install -r requirements.txt``` to fetch missing python packages...

## Usage

### Command Line

See the console section for the commands
 
```

  iBrew Web Server

  Usage: iBrew (dump) (fahrenheid) web (port) (host)

    web                    start web interface & rest api
    port                   optional port number, default 2082


  iBrew Command Line

  Usage: iBrew (dump) (shout|slow) (coffee|kettle) (fahrenheid) [command] (host)

    dump                   dump message enabled
    shout                  sends commands and quits not waiting for a reply
    slow                   fully inits everything before action
    coffee                 assumes coffee machine
    kettle                 assumes kettle
    command                action to take!
    fahrenheid             use fahrenheid
    host                   host address (format: ip4, ip6, fqdn)

  If you do not supply a host, it will try to connect to the first detected device
  Thus if you have more then one device supply a host (if its not in direct mode)


```

### Console
Start the console with the command `iBrew console`. The following commands are available within the console,
you can also use them on the command line as arguments:

```

  iKettle 2.0 & Smarter Coffee  Commands
    default                set default settings
    info                   device info
    history                action history
    list                   list detected devices
    reset                  reset device to default
    start                  start the device
    status                 show status
    settings               show user settings
    stop                   stop the appliance
    time [time]            set the device time

  iKettle 2.0 Commands
    base                   show watersensor base value
    base [base]            store watersensor base value
    calibrate              calibrates watersensor
    celsius                use celsius ºC [console only]
    fahrenheid             use fahrenheid ºF [console only]
    formula (temperature (keepwarm))] heat kettle in formula mode
    heat (temperature)(keepwarm))    heat kettle
    stop kettle            stops heating
    settings [temperature] [keepwarm] [formula] [formulatemperature] store kettle user settings

  Smarter Coffee  Commands
    brew (cups (hotplate (grind (strength)))) brew coffee
    brew default           brew coffee with default settings
    carafe                 returns if carafe is required
    carafe [state]         set carafe is required [on or off]
    cups [number]          set number of cups [1..12]
    beans                  use beans as grinded source
    filter                 use filter as grinded source
    hotplate off           turn hotplate off
    hotplate on (minutes)  turn hotplate on (time in minutes)
    singlecup              return single coffee cup mode
    singlecup [state]      set single coffee cup mode [on or off]
    (strength) [strength]  set strength coffee [weak, medium or strong]
    stop coffee            stops brewing
    settings [cups] [hotplate] [grind] [strength] store user settings
    timer [time]           add timer
    timers                 show timers

  Wireless Network Commands
    direct                 enable direct mode access
    join [net] [pass]      connect to wireless network
    rejoin                 rejoins current wireless network [not in direct mode]
    scan                   scan wireless networks

  Debug Commands
    [hexdata]              send raw data to device (e.g. '64 7e')
    dump                   toggle 'dump raw messages'
    console                start console [command line only]
    connect [host]         connect to device [console only]
    firmware               show firmware Wifi
    monitor                monitor incomming traffic
    protocol               show all protocol information available
    stats                  show traffic statistics
    sweep (id)             [developer only] try (all or start with id) unknown command codes

  Debug Protocol Help Commands
    examples               show examples of commands
    messages               show all known protocol messages
    message [id]           show protocol message detail of message [id]
    notes                  show developer notes on the devices
    structure              show protocol structure information

  iBrew Commands
    joke                   show joke
    license                show license
    license disagree       stop using license [command line only]
    quit                   quit console [console only]


```

#### Examples

```

  Example:
    off            Stop heating/brewing
    messages       Show all protocol messages
    message 3e     Show protocol message 3a, turn hotplate on
    167E           Send kettle raw stop
    21 30 05 7e    Send kettle raw heat
    strength weak  Set coffee strength to weak
    cups 3         Set number of cups to brew


```


### Web Interface

This is a build in progress, please contribute!

Start the web interface and surf to:

```
http://ip:port/
```

#### REST API

You can find information on the rest api under:

```
http://ip:port/info/api
```
 
     
### LICENSE

The author has no contact with or support from Smarter, and is not affiliated in any way with the company that produces the appliances.


Copyright (c) 2016, Tristan Crispijn
All rights reserved.

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. You may not use source, binary forms or derivative work, with or without modification, for commercial purposes. 

4. Written consent of the original author with his/her signature on paper.


THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE. YOU AGREE TO NOT USE THIS SOFTWARE IN ANY WAY. SMARTER EMPLOYEES OR SMARTER AFFILIATED PEOPLE ARE NOT ALLOWED TO USE THIS SOFTWARE OR DERIVATIVE WORK. YOU AGREE THAT THE SOFTWARE CAN MONITOR THE USAGE OF THE SOFTWARE ITSELF AND OR THE DEVICES ATTACHED TO THE SOFTWARE, AND SEND IT BACK TO A MONITOR SERVER FOR BETTER SUPPORT. ENJOY!
               
