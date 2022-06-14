# Testing

## Hardware

CPU: Broadcom BCM2711, Quad-Core-Cortex-A72 (ARM Version 8), 64-Bit-SoC (System-on-a-Chip) @ 1,5 GHz

CACHES: 32kB data + 48kB instruction L1 cache per core, 1MB L2 cache

MEMORY: 4 GB LPDDR4-2400-SDRAM

## Ziel der Reproduktion

- Möglich Optionen: `inference_time`, `total_energy_consumption`, `total_temp`

## Experimente

### Experiment 1

Bei diesem Experiment wird Tabelle 2 (Energieverbrauch für `Xception`) reproduziert.

```sh
docker-compose exec unicorn python ./tests/run_unicorn_debug.py -o total_energy_consumption -s Image -k Xavier -m offline
```

#### Macbook

##### Unicorn

```sh
Connections discovered by the causal graph
[('branch-load-misses', 'raw_syscalls_sys_exit'), ('cache-misses', 'total_energy_consumption'), ('cache-misses', 'major-faults'), ('context-switches', 'raw_syscalls_sys_enter'), ('emc_freq', 'L1-dcache-load-misses'), ('branch-loads', 'sched_sched_overutilized'), ('branch-loads', 'sched_sched_switch'), ('branch-misses', 'L1-dcache-loads'), ('instructions', 'branch-loads'), ('sched_sched_stat_runtime', 'instructions'), ('cycles', 'raw_syscalls_sys_enter'), ('sched_sched_switch', 'minor-faults'), ('L1-dcache-stores', 'raw_syscalls_sys_exit'), ('kernel.sched_latency_ns', 'L1-dcache-loads'), ('branch-load-misses', 'total_energy_consumption'), ('cache-misses', 'total_energy_consumption'), ('cache-misses', 'total_energy_consumption'), ('context-switches', 'total_energy_consumption'), ('emc_freq', 'total_energy_consumption'), ('branch-loads', 'total_energy_consumption'), ('branch-loads', 'total_energy_consumption')]
--------------------------------------------------------------
[['total_energy_consumption', 'core_freq'], ['total_energy_consumption', 'emc_freq'], ['total_energy_consumption', 'migrations'], ['total_energy_consumption', 'kernel.max_pids'], ['total_energy_consumption', 'minor-faults'], ['total_energy_consumption', 'vm.swappiness'], ['total_energy_consumption', 'logical_devices'], ['total_energy_consumption', 'emc_freq'], ['total_energy_consumption', 'logical_devices']]
--------------------------------------------------
--------------------------------------------------
             Recommended Configuration
memory_growth                    5.000000e-01
logical_devices                  1.000000e+00
core_freq                        1.574400e+06
gpu_freq                         1.651200e+06
emc_freq                         2.133000e+09
num_cores                        2.000000e+00
scheduler.policy                 1.000000e+00
vm.swappiness                    1.000000e+02
vm.vfs_cache_pressure            5.000000e+02
vm.dirty_background_ratio        8.000000e+01
vm.drop_caches                   3.000000e+00
vm.nr_hugepages                  1.000000e+00
vm.overcommit_ratio              5.000000e+01
vm.overcommit_memory             1.000000e+00
vm.overcommit_hugepages          2.000000e+00
kernel.sched_child_runs_first    0.000000e+00
kernel.sched_rt_runtime_us       5.000000e+05
vm.dirty_bytes                   3.000000e+01
vm.dirty_background_bytes        6.000000e+01
vm.dirty_ratio                   5.000000e+00
swap_memory                      1.000000e+00
kernel.max_pids                  6.553600e+04
kernel.sched_latency_ns          2.400000e+07
kernel.sched_nr_migrate          2.560000e+02
kernel.cpu_time_max_percent      5.000000e+01
kernel.sched_time_avg_ms         1.000000e+03
Name: 0, dtype: float64
--------------------------------------------------
--------------------------------------------------
--------------------------------------------------
+++++++++++++++Recommended Fix++++++++++++++++++++
memory_growth                    5.000000e-01
logical_devices                  1.000000e+00
core_freq                        1.574400e+06
gpu_freq                         1.651200e+06
emc_freq                         2.133000e+09
num_cores                        2.000000e+00
scheduler.policy                 1.000000e+00
vm.swappiness                    1.000000e+02
vm.vfs_cache_pressure            5.000000e+02
vm.dirty_background_ratio        8.000000e+01
vm.drop_caches                   3.000000e+00
vm.nr_hugepages                  1.000000e+00
vm.overcommit_ratio              5.000000e+01
vm.overcommit_memory             1.000000e+00
vm.overcommit_hugepages          2.000000e+00
kernel.sched_child_runs_first    0.000000e+00
kernel.sched_rt_runtime_us       5.000000e+05
vm.dirty_bytes                   3.000000e+01
vm.dirty_background_bytes        6.000000e+01
vm.dirty_ratio                   5.000000e+00
swap_memory                      1.000000e+00
kernel.max_pids                  6.553600e+04
kernel.sched_latency_ns          2.400000e+07
kernel.sched_nr_migrate          2.560000e+02
kernel.cpu_time_max_percent      5.000000e+01
kernel.sched_time_avg_ms         1.000000e+03
Name: 0, dtype: float64
Unicorn Fix Value 26678
Number of Samples Required 26
--------------------------------------------------
--------------------------------------------------
+++++++++++++++++++++Bug++++++++++++++++++++++++++
memory_growth                            0.5
logical_devices                          1.0
core_freq                          1651200.0
gpu_freq                           1651200.0
emc_freq                         800000000.0
num_cores                                2.0
scheduler.policy                         1.0
vm.swappiness                          100.0
vm.vfs_cache_pressure                  500.0
vm.dirty_background_ratio               80.0
vm.drop_caches                           3.0
vm.nr_hugepages                          1.0
vm.overcommit_ratio                     50.0
vm.overcommit_memory                     1.0
vm.overcommit_hugepages                  2.0
kernel.sched_child_runs_first            0.0
kernel.sched_rt_runtime_us          500000.0
vm.dirty_bytes                          30.0
vm.dirty_background_bytes               60.0
vm.dirty_ratio                           5.0
swap_memory                              1.0
kernel.max_pids                      32768.0
kernel.sched_latency_ns           24000000.0
kernel.sched_nr_migrate                256.0
kernel.cpu_time_max_percent             50.0
kernel.sched_time_avg_ms              1000.0
Name: 28, dtype: float64
Bug Objective Value 141401
--------------------------------------------------
```

##### CBI

```sh
++++++++++++++++++++++++++++++++++++++++++++++++++
Recommended Fix
(memory_growth                           0.5
logical_devices                           1
core_freq                           2265600
gpu_freq                            2112000
emc_freq                         1866000000
num_cores                                 4
scheduler.policy                          1
vm.swappiness                           100
vm.vfs_cache_pressure                   100
vm.dirty_background_ratio                10
vm.drop_caches                            0
vm.nr_hugepages                           1
vm.overcommit_ratio                      60
vm.overcommit_memory                      1
vm.overcommit_hugepages                   1
kernel.sched_child_runs_first             0
kernel.sched_rt_runtime_us           500000
vm.dirty_bytes                           60
vm.dirty_background_bytes                60
vm.dirty_ratio                           50
swap_memory                               1
kernel.max_pids                       32768
kernel.sched_latency_ns            96000000
kernel.sched_nr_migrate                 128
kernel.cpu_time_max_percent              50
kernel.sched_time_avg_ms               1000
dtype: object, 0)
Recommended Fix value 28    59293
Name: total_energy_consumption, dtype: int64
++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++
Bug
core_freq                        1.651200e+06
gpu_freq                         1.651200e+06
emc_freq                         8.000000e+08
num_cores                        2.000000e+00
memory_growth                    5.000000e-01
logical_devices                  1.000000e+00
scheduler.policy                 1.000000e+00
vm.swappiness                    1.000000e+02
vm.vfs_cache_pressure            5.000000e+02
vm.dirty_background_ratio        8.000000e+01
vm.drop_caches                   3.000000e+00
vm.nr_hugepages                  1.000000e+00
vm.overcommit_ratio              5.000000e+01
vm.overcommit_memory             1.000000e+00
vm.overcommit_hugepages          2.000000e+00
kernel.sched_child_runs_first    0.000000e+00
kernel.sched_rt_runtime_us       5.000000e+05
vm.dirty_bytes                   3.000000e+01
vm.dirty_background_bytes        6.000000e+01
vm.dirty_ratio                   5.000000e+00
swap_memory                      1.000000e+00
kernel.max_pids                  3.276800e+04
kernel.sched_latency_ns          2.400000e+07
kernel.sched_nr_migrate          2.560000e+02
kernel.cpu_time_max_percent      5.000000e+01
kernel.sched_time_avg_ms         1.000000e+03
inference_time                   1.618297e+01
total_energy_consumption         1.414016e+05
Name: 28, dtype: float64
++++++++++++++++++++++++++++++++++++++++++++++++++
```

##### encore

```sh
Processing 628 combinations | Sampling itemset size 4 3
++++++++++++++++++++++++++++++++++++++++++++++++++
Recommended Fix
memory_growth                            0.5
logical_devices                          1.0
core_freq                          1651200.0
gpu_freq                           1651200.0
emc_freq                         800000000.0
num_cores                                2.0
scheduler.policy                         1.0
vm.swappiness                          100.0
vm.vfs_cache_pressure                  500.0
vm.dirty_background_ratio               80.0
vm.drop_caches                           3.0
vm.nr_hugepages                          1.0
vm.overcommit_ratio                       60
vm.overcommit_memory                     1.0
vm.overcommit_hugepages                  2.0
kernel.sched_child_runs_first            0.0
kernel.sched_rt_runtime_us          500000.0
vm.dirty_bytes                          30.0
vm.dirty_background_bytes               60.0
vm.dirty_ratio                           5.0
swap_memory                              1.0
kernel.max_pids                      32768.0
kernel.sched_latency_ns           24000000.0
kernel.sched_nr_migrate                  256
kernel.cpu_time_max_percent             50.0
kernel.sched_time_avg_ms              1000.0
dtype: object
Recommended Fix value 57    70637
Name: total_energy_consumption, dtype: int64
++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++
Bug
core_freq                        1.651200e+06
gpu_freq                         1.651200e+06
emc_freq                         8.000000e+08
num_cores                        2.000000e+00
memory_growth                    5.000000e-01
logical_devices                  1.000000e+00
scheduler.policy                 1.000000e+00
vm.swappiness                    1.000000e+02
vm.vfs_cache_pressure            5.000000e+02
vm.dirty_background_ratio        8.000000e+01
vm.drop_caches                   3.000000e+00
vm.nr_hugepages                  1.000000e+00
vm.overcommit_ratio              5.000000e+01
vm.overcommit_memory             1.000000e+00
vm.overcommit_hugepages          2.000000e+00
kernel.sched_child_runs_first    0.000000e+00
kernel.sched_rt_runtime_us       5.000000e+05
vm.dirty_bytes                   3.000000e+01
vm.dirty_background_bytes        6.000000e+01
vm.dirty_ratio                   5.000000e+00
swap_memory                      1.000000e+00
kernel.max_pids                  3.276800e+04
kernel.sched_latency_ns          2.400000e+07
kernel.sched_nr_migrate          2.560000e+02
kernel.cpu_time_max_percent      5.000000e+01
kernel.sched_time_avg_ms         1.000000e+03
inference_time                   1.618297e+01
total_energy_consumption         1.414016e+05
Name: 28, dtype: float64
++++++++++++++++++++++++++++++++++++++++++++++++++
````

##### bugdoc

```sh
++++++++++++++++++++++++++++++++++++++++++++++++++
Recommended Fix
memory_growth                            0.5
logical_devices                          1.0
core_freq                          1651200.0
gpu_freq                            499200.0
emc_freq                         800000000.0
num_cores                                2.0
scheduler.policy                         1.0
vm.swappiness                          100.0
vm.vfs_cache_pressure                  500.0
vm.dirty_background_ratio               80.0
vm.drop_caches                           3.0
vm.nr_hugepages                          1.0
vm.overcommit_ratio                     50.0
vm.overcommit_memory                     1.0
vm.overcommit_hugepages                  2.0
kernel.sched_child_runs_first            0.0
kernel.sched_rt_runtime_us          500000.0
vm.dirty_bytes                          60.0
vm.dirty_background_bytes               60.0
vm.dirty_ratio                           5.0
swap_memory                              1.0
kernel.max_pids                      32768.0
kernel.sched_latency_ns           24000000.0
kernel.sched_nr_migrate                256.0
kernel.cpu_time_max_percent             50.0
kernel.sched_time_avg_ms              1000.0
dtype: float64
Recommended Fix Value 49706
++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++
Bug
core_freq                        1.651200e+06
gpu_freq                         1.651200e+06
emc_freq                         8.000000e+08
num_cores                        2.000000e+00
memory_growth                    5.000000e-01
logical_devices                  1.000000e+00
scheduler.policy                 1.000000e+00
vm.swappiness                    1.000000e+02
vm.vfs_cache_pressure            5.000000e+02
vm.dirty_background_ratio        8.000000e+01
vm.drop_caches                   3.000000e+00
vm.nr_hugepages                  1.000000e+00
vm.overcommit_ratio              5.000000e+01
vm.overcommit_memory             1.000000e+00
vm.overcommit_hugepages          2.000000e+00
kernel.sched_child_runs_first    0.000000e+00
kernel.sched_rt_runtime_us       5.000000e+05
vm.dirty_bytes                   3.000000e+01
vm.dirty_background_bytes        6.000000e+01
vm.dirty_ratio                   5.000000e+00
swap_memory                      1.000000e+00
kernel.max_pids                  3.276800e+04
kernel.sched_latency_ns          2.400000e+07
kernel.sched_nr_migrate          2.560000e+02
kernel.cpu_time_max_percent      5.000000e+01
kernel.sched_time_avg_ms         1.000000e+03
inference_time                   1.618297e+01
total_energy_consumption         1.414016e+05
Name: 28, dtype: float64
++++++++++++++++++++++++++++++++++++++++++++++++++
Number of Samples required: 266
```
