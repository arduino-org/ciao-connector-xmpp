# Ciao Connector XMPP
XMPP Connector for Arduino Ciao - Connect to an Jabber Server for send and receive messages

## Installation
### Linino OS
Open a `secure shell` to your board and login into **Linino OS**.
Install it via `opkg` running this commands:
```
$ opkg update
$ opkg install ciao-connector-xmpp
```

### Arduino OS
If you have **Arduino OS** installed in your
board you can use **Arduino Package Manager Application**.
Go to	*Menu -> Arduino -> Arduino Package Manger*
and then search `ciao-connector-xmpp`, select it an press *Install*

## Manually
Download the zip file of the latest [release](https://github.com/arduino-org/ciao-connector-xmpp/releases),
unzip and move it via `scp` inside you board in the desired location.
**Be sure to move `smtp.ciao.conf.json` file into the ciao directory**, eg:
```
$ scp ~/Downloads/ciao-connector-xmpp/xmpp.ciao.conf.json root@arduino.local:/usr/lib/python2.7/ciao/conf/
$ scp -r ~/Downloads/ciao-connector-xmpp/xmpp root@arduino.local:/root/.ciao/
```

## Configuration

### Ciao Core Configuration
Before start using the connector, set to `true` the `enabled` key in the `xmpp.ciao.json.conf` file.
Change the `commands/start` values only if you installed the connector manually.

```json
{
	"name" : "xmpp",
	"enabled": false,
	"type" : "managed",
	"core" : ">=0.0.2",
	"commands": {
		"start": ["/root/.ciao/xmpp/xmpp.py"],
		"stop": ["/usr/bin/killall","-s", "HUP","xmpp.py"]
	},
	"implements" : {
		"read" : { "direction": "in", "has_params": false },
		"write" : { "direction": "out", "has_params": true },
		"writeresponse" : { "direction": "out", "has_params": true }
	}
}
```

### Connector Configuration/Parameters
To customize the connector to use your email account,
please insert the correct vaules in the configuration
file `xmpp/xmpp.json.conf`:

```json
...
"params" : {
	"host" : "YOUR_XMPP_IP_OR_HOSTNAME",
	"domain" : "ACCOUNT_DOMAIN",
	"port" : 5222,
	"username" : "USERNAME",
	"password" : "PASSWORD",
	"tls" : false,
	"ssl" : false
},
...
```
## How To Use
Open [Arduino IDE](http://www.arduino.org/software), import
Arduino Ciao Library in your sketch and take a look at the
[example](https://github.com/arduino-org/ciao-connector-xmpp/examples)

## See Also
[Arduino Ciao](http://labs.arduino.org/Ciao)
