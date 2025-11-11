---
author: "davidalvarezp"
title: "Optimización y tuning de Redis y Memcached"
slug: "optimizar-redis-memcached"
description: "Aprende técnicas avanzadas para mejorar el rendimiento de bases de datos en memoria como Redis y Memcached."
tags: ["Redis", "Memcached", "Bases de datos", "Rendimiento"]
categories: ["SysAdmin"]
date: "2025-11-05"
keywords: ["redis", "memcached", "tuning", "optimización", "cache"]
draft: false
---

# Optimización y tuning de Redis y Memcached

Redis y Memcached son **bases de datos en memoria** que aceleran el acceso a datos críticos. Para maximizar su rendimiento, se requiere un tuning cuidadoso y monitoreo de métricas.

## Configuración de Redis

Parámetros importantes en `redis.conf`:
```text
maxmemory 2gb
maxmemory-policy allkeys-lru
appendonly yes
save 900 1
save 300 10
save 60 10000
```

Monitoreo de uso de memoria:
```bash
redis-cli INFO memory
redis-cli MONITOR
```

## Configuración de Memcached

Iniciar Memcached con parámetros ajustados:
```bash
memcached -m 1024 -p 11211 -u memcache -c 1024 -d
```

Monitoreo de stats:
```bash
echo stats | nc localhost 11211
```

## Buenas prácticas

- Ajustar políticas de expiración y tamaño de caché
- Evitar operaciones pesadas de persistencia en memoria
- Monitorear latencia y tasas de hits/misses
- Integrar métricas con Prometheus/Grafana para alertas

## Conclusión

Un tuning adecuado de Redis y Memcached asegura **alto rendimiento y baja latencia** para aplicaciones críticas, manteniendo la escalabilidad.
