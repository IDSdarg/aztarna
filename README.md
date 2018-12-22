# aztarna
<a href="http://www.aliasrobotics.com"><img src="https://aliasrobotics.com/media/alias_logo_central.png" align="left" hspace="8" vspace="2" width="200"></a>

This repository contains Alias Robotics' aztarna, a footprinting tool for robots.

**Alias Robotics supports original robot manufacturers assessing their security and improving their quality of software. By no means we encourage or promote the unauthorized tampering with running robotic systems. This can cause serious human harm and material damages.**


### For ROS
* A list of the ROS nodes present in the system (Publishers and Subscribers)
* For each node, the published and subscribed topis including the topic type
* For each node, the ROS services each of the nodes offer
* A list of all ROS parameters present in the Parameter Server
* A list of the active communications running in the system. A single communication includes the involved publiser/subscriber nodes and the topics

### For SROS
* Determining if the system is a SROS master.
* Detecting if demo configuration is in use.
* A list of the nodes found in the system. (Extended mode)
* A list of allow/deny policies for each node.
  * Publishable topics.
  * Subscriptable topics.
  * Executable services.
  * Readable parameters.

### For Industrial routers
* Detecting eWON webserver.
  * Check if the webserver has default credentials.


## Installing
### For production
```
pip3 install .
```
or
```
python3 setup.py install
```

### For development
```
pip3 install -e .
```
or
```
python3 setup.py develop
```
The only requirement is [setuptools](https://pypi.org/project/setuptools/) package, which is usually a defacto standard in a python3 installation.

### Install with docker
```bash
docker build -t aztarna_docker .
```

### Code usage:

```bash
usage: aztarna [-h] -t TYPE [-a ADDRESS] -p PORTS [-i INPUT_FILE]
               [-o OUT_FILE] [-e EXTENDED]

Aztarna

optional arguments:
  -h, --help            show this help message and exit
  -t TYPE, --type TYPE  <ROS/SROS> Scan ROS or SROS hosts
  -a ADDRESS, --address ADDRESS
                        Single address or network range to scan.
  -p PORTS, --ports PORTS
                        Ports to scan (format: 13311 or 11111-11155 or
                        1,2,3,4)
  -i INPUT_FILE, --input_file INPUT_FILE
                        Input file of addresses to use for scanning
  -o OUT_FILE, --out_file OUT_FILE
                        Output file for the results
  -e EXTENDED, --extended EXTENDED
                        Extended scan of the hosts
  -r RATE, --rate RATE
                        Maximum simultaneous network connections
```

### Run the code (example input file):

```bash
aztarna -t ROS -p 11311 -i ros_scan_s20.csv
```

### Run the code with Docker (example input file):
```bash
docker run -v <host_path>:/root -it aztarna_docker -t ROS -p 11311 -i <input_file>
```

### Run the code (example single ip address):

```bash
aztarna -t ROS -p 11311 -a 115.129.241.241
```

### Run the code (example subnet):

```bash
aztarna -t ROS -p 11311 -a 115.129.241.0/24
```

### Run the code (example single ip address, port range):

```bash
aztarna -t ROS -p 11311-11500 -a 115.129.241.241
```

### Run the code (example single ip address, port list):

```bash
aztarna -t ROS -p 11311,11312,11313 -a 115.129.241.241
```

### Run the code (example piping directly from zmap):

```bash
zmap -p 11311 0.0.0.0/0 -q | aztarna -t SROS -p 11311
```
