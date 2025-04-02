#  Проект мониторинга с Prometheus и Grafana

## Запуск и доступ к сервисам

### 1 Установка зависимостей

```bash
brew install vagrant
brew install qemu
brew install ansible
```
 *VirtualBox не работает с архитектурой arm64, поэтому в качестве провайдера использован qemu.*

---
### 2 Запуск сервисов:
```bash
vagrant up --provider=qemu
```

### 3 Доступ к сервисам:
- **Grafana**: [http://localhost:3000](http://localhost:3000)
- **Prometheus**: [http://localhost:9090](http://localhost:9090)

---

## Структура проекта
```
.
├── README.md
├── ansible
│   ├── files
│   │   ├── dashboards.yml
│   │   ├── data-source.yml
│   │   ├── docker-compose.yml
│   │   ├── grafana-dash.json
│   │   └── prometheus.yml
│   ├── playbook.yml
│   └── roles
│       ├── docker
│       │   └── tasks
│       │       └── main.yml
│       ├── grafana
│       │   └── tasks
│       │       └── main.yml
│       ├── node_exporter
│       │   └── tasks
│       │       └── main.yml
│       └── prometheus
│           └── tasks
│               └── main.yml
└── Vagrantfile
```

---


## Описание плейбука

### Используемые роли:

- **Docker**: Устанавливает зависимости, Docker, Docker Compose, создает папку `/opt/monitoring`.
- **Node_exporter**: Устанавливает и запускает `node_exporter` в качестве systemd-сервиса на хост-машине.
- **Prometheus**: Копирует конфигурацию Prometheus, запускает контейнер.
- **Grafana**: Создает директорию для конфигурационных файлов, копирует их и запускает контейнер.

---

