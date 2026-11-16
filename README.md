# Домашнее задание 4. Notification Platform

## Что где

- [requirements.md](requirements.md): задания 1-7. Требования, ASR, архитектурные вопросы, последствия, неподходящие решения, риски.
- [rfc.md](rfc.md): задание 8. RFC по гарантированной доставке критичных уведомлений с failover между каналами.
- [diagrams](diagrams): исходники PlantUML (C4 Container, sequence, машина состояний) и отрисованные SVG.

## Решения

- Транзакционные уведомления отключить нельзя, можно выбрать основной канал. Маркетинг только по согласию.
- Канальный план: push, через 15 с без подтверждения SMS, затем email. Для подозрительных операций push и SMS сразу.
- Рассмотрены два варианта: оркестратор на Kafka и PostgreSQL, и Temporal. Выбран первый: хватает по нагрузке, стек уже эксплуатируется, меньше операционный риск.

## Перерисовать диаграммы

```bash
docker run --rm -v "$PWD/diagrams":/data -w /data plantuml/plantuml:1.2026.2 -tsvg -charset UTF-8 a-c4.puml a-seq-main.puml a-seq-failover.puml b-c4.puml b-seq-main.puml b-seq-failover.puml state-machine.puml
```
