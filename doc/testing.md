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
