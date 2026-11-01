# EdgeAI-Monitor

A Python-based monitoring and analysis framework for collecting **system telemetry during MLPerf benchmarks**.

The framework synchronizes hardware and external power measurements with the MLPerf LoadGen benchmark interval and produces:

- Raw monitoring data in JSON
- Flattened monitoring data in CSV
- Benchmark-only CSV data
- Benchmark summary JSON
- Benchmark performance/telemetry plots

The framework is designed primarily for an **Intel Linux host** running MLPerf through a Docker/container environment, with external wall-power measurements obtained from a **Tasmota-compatible power monitoring plug**.

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

to run the framework with 6 threads

the following commands is used

python3 wrapper.py   --idle 30   --cooldown 20   --interval 1   --csv trace.csv   --json trace.json   --cmd mlcr run-mlperf,inference,_find-performance,_full,_r5.1-dev   --model=resnet50   --implementation=reference   --framework=onnxruntime   --category=edge   --scenario=Offline   --execution_mode=test   --device=cpu   --docker   --quiet   --test_query_count=1000   --rerun   --threads=6

