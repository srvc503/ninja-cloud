# NinjaCloud

Одноузловая self-hosted private cloud platform, разработанная на ограниченном
аппаратном ресурсе Intel NUC7CJYH.

## Цель проекта

Построить воспроизводимую платформу, которая предоставляет Compute, Storage и
Database capabilities, управляется через IaC и CI/CD, имеет встроенную
observability, security и disaster recovery.

## Оборудование

- **Модель:** Intel NUC7CJYH
- **CPU:** Intel Celeron J4005 (2 ядра / 2 потока, 2.0–2.7 GHz)
- **RAM:** 16 GB DDR4 (14 GiB доступно)
- **Диск:** 931.5 GB SSD (LVM)
- **ОС:** Ubuntu 26.04.1 LTS

## Архитектура

### Storage layout

| Том | Размер | Назначение |
|---|---|---|
| `/` (ubuntu-lv) | 100 GB | Система |
| `/opt/ninjacloud` | 150 GB | Сервисы, БД, конфиги, secrets |
| `/data` | 400 GB | Пользовательские данные |
| Свободно в VG | ~278 GB | Запас на будущее |

### Слои платформы

- **Infrastructure:** Ubuntu Server + Ansible (IaC)
- **Platform:** (планируется) Control Plane + API
- **Observability:** (планируется) Prometheus + Grafana + Loki
- **Backup:** (планируется) Restic + DR
- **CI/CD:** (планируется) GitHub Actions

## Статус

**v0.1** — базовая структура проекта, baseline, LVM, SSH-ключи.

## Roadmap

- [x] v0.1 — Baseline + LVM + SSH + структура проекта
- [ ] v0.2 — IaC + Security baseline + Docker
- [ ] v0.3 — First workload + metrics baseline
- [ ] v0.4 — Observability
- [ ] v0.5 — Backup + DR
- [ ] v0.6 — CI/CD
- [ ] v0.7 — Security hardening
- [ ] v0.8 — Storage + Database as Services
- [ ] v0.9 — Control Plane
- [ ] v1.0 — Private Cloud Platform

## Anti-goals

Проект осознанно ограничен одним узлом.

- **Multi-node** — не входит в scope: NUC один, симуляция распределённой системы не даёт реальных навыков
- **Kubernetes** — не используется ради галочки: на J4005 не решает реальной задачи
- **Production-grade HA** — не цель проекта: это learning/portfolio платформа

## Запуск

```bash
ansible-playbook -i ansible/inventory/hosts.ini ansible/playbooks/site.yml
