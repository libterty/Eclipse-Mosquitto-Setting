# Eclipse Mosquitto Setting

- Simple Guideline for setting Mqtt socket with docker image
- I prefer using docker to run Mqtt, but you can also download from their offical website

## Pre-Requirement

- [docker](https://www.docker.com)

### Structure file system

```bash
$ mkdir mosquitto
$ cd mosquitto
$ mkdir config
$ mkdir data
$ mkdir log
$ cd config
$ touch mosquitto.conf
$ touch passwd // If you have password setting you can add in here
```

> :memo: **A complete file structure should like this**
```
mosquitto
|-- config
|  |-- mosquitto.conf
|  |-- passwd
|-- data
|-- log
```

> :memo: **Configuring mosquitto.conf**

```bash
$ cat mosquitto.conf or vim mosquitto.conf // up to you
```

> :exclamation: **Configuring**

```
persistence true
persistence_location /mosquitto/data/
log_dest file /mosquitto/log/mosquitto.log
log_dest syslog
log_dest stdout
log_dest topic
log_type error
log_type warning
log_type notice
log_type information
connection_messages false
log_timestamp true
listener 9001
protocol websockets
```

### Docker Setup

> :memo: **Download eclipse mosquitto docker image**

```bash
$ docker pull eclipse-mosquitto
```

> :whale: **Running**

```bash
$ docker run -it --name mosquitto -p 9001:9001 -v $(pwd)/mosquitto:/mosquitto/ eclipse-mosquitto
```

> :stopwatch: **Stop mosquitto docker container**

```bash
$ docker stop mosquitto
```

> :star: **Restart mosquitto docker container**

```bash
$ docker start mosquitto
```

> :punch: **Check**
```bash=
curl --include \
     --no-buffer \
     --header "Connection: Upgrade" \
     --header "Upgrade: websocket" \
     --header "Host: 127.0.01:9001" \
     --header "Origin: http://127.0.01:9001" \
     --header "Sec-WebSocket-Key: SGVsbG8sIHdvcmxkIQ==" \
     --header "Sec-WebSocket-Version: 13" \
     http://127.0.01:9001/
```

## Author
[11](https://github.com/libterty)