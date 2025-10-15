# Мониторинг

## Kafka и брокеры

- Broker: цпу, память, файловая система, сетевая нагрузка.
- Cluster health: UnderReplicatedPartitions, OfflinePartitionsCount, ActiveControllerCount.
- Topic/partition: bytes in/out, records in/out, request-latency produce/fetch p95/p99.
- Producer: record-error-rate, record-retry-rate, batch-size-avg, compression-rate-avg.
- Consumer: lag per group/partition (Burrow + Kafka Exporter), rebalance-rate, commit latency.

## Flink и Streams

- Flink: checkpoint duration/interval, alignment time, backpressure ratio, busy time, watermarks lag, numRestarts.
- Kafka Streams: task lag, commit latency, skipped-records, standby состояние, EOS commit errors.

## Надёжность и ретраи

- Размер Retry и DLQ, скорость дренажа retry, доля сообщений, уходящих в DLQ.
- Outbox lag (insert→publish), Debezium source lag, ошибки парсинга схем.

## Сага и бизнес-метрики

- Saga success rate, средняя длительность саги, распределение по шагам, частота компенсаций.
- Pricing latency (ingest→surge.updated), средняя и p95.
- Match quality: среднее время подбора, доля отмен из-за подбора.
- Payments: авторизации/капчуры успех/ошибка, доля повторов.
- Notifications: delivered/opened/error rate (по провайдерам).

## Общее

- Trace latency: HTTP → событие → обработчик → ответ пользователю (OTel/Tempo).
- SLO/Error Budget дашборды и алерты (Booking/Payments/Pricing).

# Инструменты мониторинга

Prometheus + Alertmanager - сбор/алерты (в т.ч. JMX Exporter, Kafka Exporter, Flink Reporter).

- Grafana - дашборды (кластер, топики, потоки, бизнес SLO).
- Loki - централизованные логи (продьюсеры/консьюмеры/функции Flink).
- OpenTelemetry Collector + Tempo - распределённый трейcинг E2E.
- Burrow - мониторинг consumer lag.
- AKHQ - обзор состояния топиков/консьюмеров.
