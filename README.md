# EdgeAI-Monitor

A Python-based monitoring and analysis framework for collecting **system telemetry during MLPerf benchmarks execution**.

The framework synchronizes hardware and external power measurements with the MLPerf LoadGen benchmark interval and produces:

- Raw monitoring data in JSON
- Flattened monitoring data in CSV
- Benchmark-only CSV data
- Benchmark summary JSON
- Benchmark performance/telemetry plots

Mainly, the framework is designed for an **Intel and NVIDIA Linux host** running MLPerf through a Docker/container environment, with external wall-power measurements obtained from a **P11 power monitoring smart plug**.

---

# 1. Overview

The purpose of this project is to measure the relationship between:

- MLPerf benchmark execution
- CPU utilization
- CPU frequency
- CPU temperature
- Intel RAPL energy
- Intel RAPL power
- External AC wall power
- Voltage
- Current
- Power factor
- Memory utilization

The most important feature is the synchronization between the MLPerf benchmark interval and the monitoring data.

The framework attempts to identify:

```text
MLPerf benchmark START
        |
        v
+-----------------------+
| Benchmark measurement |
|       interval        |
+-----------------------+
        |
        v
MLPerf benchmark END
```text

---
......

python3 -m pip install pexpect

for raspberry pi version : 4.9.0 is used
..........

python3 -m pip install psutil

for rpi: 7.2.2
............
for the rpi

cat /etc/os-release

PRETTY_NAME="Debian GNU/Linux 13 (trixie)"
NAME="Debian GNU/Linux"
VERSION_ID="13"
VERSION="13 (trixie)"
VERSION_CODENAME=trixie
DEBIAN_VERSION_FULL=13.5
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"

......

uname -m
aarch64

..........

id
uid=1000(sara) gid=1000(sara) groups=1000(sara),4(adm),20(dialout),24(cdrom),27(sudo),29(audio),44(video),46(plugdev),60(games),100(users),102(netdev),108(lpadmin),986(gpio),988(i2c),989(spi),992(render),996(input)

...........

Docker

docker --version

sudo apt update

sudo apt install -y ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/debian/gpg \
-o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker --version

for the rpi: Docker version 29.9.2, build a82e528

sudo systemctl status docker

sudo usermod -aG docker sara




............


```text
python3 wrapper.py   --idle 30   --cooldown 20   --interval 1   --csv trace.csv   --json trace.json   --cmd mlcr run-mlperf,inference,_find-performance,_full,_r5.1-dev   --model=resnet50   --implementation=reference   --framework=onnxruntime   --category=edge   --scenario=Offline   --execution_mode=test   --device=cpu   --docker   --quiet   --test_query_count=1000   --rerun   --threads=6

