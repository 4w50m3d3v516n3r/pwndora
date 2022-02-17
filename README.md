<p align="center">
<img src="images/final1.png" width=200px>
</p>
<p align="center">

<img src="https://github.com/aleen42/badges/blob/master/src/elasticsearch.svg">
<img src="https://github.com/aleen42/badges/blob/master/src/kibana.svg">
<img src="https://github.com/aleen42/badges/blob/master/src/python.svg">
<img src="https://github.com/aleen42/badges/blob/master/src/docker.svg">
<img src="https://img.shields.io/badge/Version-3.0-brightgreen">
<img src="https://img.shields.io/badge/Maintained%3F-yes-blue.svg">

</p>

## Introduction
Pwndora is a massive and fast IPv4 address range scanner, integrated with multi-threading.

Using sockets, it analyzes which ports are open, and collects more information about targets, each result is stored in Elasticsearch. You can integrate with Kibana to be able to visualize and manipulate data, basically it's like having your own IoT search engine at home.

## Features

- Port scanning with different options and retrieve software banner information.
- Detect some web technologies running on servers, using [Webtech](https://github.com/ShielderSec/webtech) integration.   
- Retrieves IP geolocation from Maxmind free database, updated periodically. 
- Anonymous login detection on FTP servers.
- Send notifications with results using Slack API.

## Visual
<a href="https://asciinema.org/a/469844" target="_blank"><img src="https://asciinema.org/a/n1RmVV8Rq800jQlCih8ROWeaY.svg" width=700px /></a>

## Getting Started
  > Make sure you have $HOME/.local/share directory, to avoiding issues with Webtech.
  
  > To use slack argument, you should configure [Incoming Webhooks](https://api.slack.com/messaging/webhooks) URL in config.py
- Clone this repository
- Install requirements with Python PIP
- Set password for Elasticsearch and Kibana containers in [docker-compose.yml](https://github.com/alechilczenko/pwndora/blob/main/scanner/Connect.py)
- Configure connection to Elasticsearch in [connect.py](https://github.com/alechilczenko/pwndora/blob/main/scanner/Connect.py)
- Set paths of Maxmind ASN, city databases and Rendertron URL in [config.py](https://github.com/alechilczenko/pwndora/blob/main/scanner/config.py)
- Launch containers in background with Docker Compose.
- Finally start scanner

## Usage
```
options:
  -h, --help            show this help message and exit
  -s START, --start START
                        Start IPv4 address
  -e END, --end END     End IPv4 address
  -t THREADS, --threads THREADS
                        Number of threads [Default: 50]
  -m FILE, --massive-scan FILE
                        File path with IPv4 ranges
  -ti TIMEOUT, --timeout TIMEOUT
                        Socket timeout [Default: 0.5]
  -p, --top-ports       Scan only 20 most used ports [Default]
  -a, --all-ports       Scan 1000 most used ports
  -c CUSTOM [CUSTOM ...], --custom-ports CUSTOM [CUSTOM ...]
                        Scan custom ports directly from terminal
  -sl, --slack          Send notifications by Slack with results
```
## Examples
> If this is your first time running, you should use the --update argument.

Scan only a single IPv4 address range:
```shell
python3 CLI.py -s 192.168.0.0 -e 192.168.0.255 -t 150 --top-ports
```
Scan from a text file with multiple IPv4 address ranges:
```shell
python3 CLI.py -m Argentina.csv -t 200 -ti 5 --all-ports
```

> If you use an excessive amount of threads, some ISPs may detect suspicious traffic and disconnect you from the network.
## Kibana Example
<img src="images/kibana1.png">

## Contributing
If you have ideas or future features, feel free to participate to continue making this project great. 

## Contact
alechilczenko@gmail.com

## Legal Disclaimer
This project is made for educational and ethical testing purposes only. Usage of this software for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program. 

## License
[Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)
