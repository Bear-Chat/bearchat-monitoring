# Monitoring with Grafana, Prometheus and Node Exporter

<div align="right">

  🇧🇷 [Versão em Português](#monitoramento-com-grafana-prometheus-e-node-exporter)

</div>

This project provides a complete monitoring environment using Docker Compose with:

- [Grafana](https://grafana.com/)
- [Prometheus](https://prometheus.io/)
- [Node Exporter](https://github.com/prometheus/node_exporter)

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/JPabloVM/infra-monitoring-kit.git
cd infra-monitoring-kit
```

### 2. Start the containers

```bash
docker-compose up -d
```

> This will create and start Prometheus, Grafana and Node Exporter services.

---

## 🔎 Access

- **Grafana**: [http://localhost:9091](http://localhost:9091)
  - Username: `admin`
  - Password: `admin` (you will be asked to change it on first login)

- **Prometheus**: [http://localhost:9095](http://localhost:9095)

- **Node Exporter**: [http://localhost:9100](http://localhost:9100)

---

## 🧠 Project Structure

```bash
.
├── docker-compose.yml
├── prometheus.yml                        # Prometheus configuration
└── grafana/
    └── provisioning/
        ├── datasources/
        │   └── prometheus.yml            # Grafana datasource (Prometheus)
        └── dashboards/
            ├── dashboards.yml            # Auto-provisioning dashboards
            └── node-exporter-full.json   # Official Node Exporter dashboard
```

---

## ✅ First Access to Grafana

1. Access [Grafana](http://localhost:9091)
2. Login using `admin / admin`
3. Check that:
   - A **Data Source** named `DS_PROMETHEUS` was created
   - The **Node Exporter dashboard** is listed on the sidebar
4. Done! Live metrics should be visible.

---

## ➕ Adding New Dashboards

1. Place your dashboard JSON file in:
   ```
   grafana/provisioning/dashboards/
   ```
2. Ensure `dashboards.yml` points to that folder:
   ```yaml
   options:
     path: /var/lib/grafana/dashboards
   ```
3. Restart the Grafana container:

   ```bash
   docker-compose restart grafana
   ```

> The new dashboard will be imported automatically.

---

## 🔌 Adding New Services to Monitor

1. Edit the `prometheus.yml` file
2. Add a new `job_name` with the desired `targets`. Example:

   ```yaml
   scrape_configs:
     - job_name: 'my-service'
       static_configs:
         - targets: ['my-service:8080']
   ```

3. Restart Prometheus:

   ```bash
   docker-compose restart prometheus
   ```

---

## 🧼 Resetting All Data

To reset everything (useful for development/testing):

```bash
docker-compose down -v
docker volume prune -f
```

---

## 📦 Requirements

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose v2+](https://docs.docker.com/compose/)

---

## 🛠️ To-do / Future Improvements

- Add Prometheus/Grafana alerting
- Export dashboards as code
- Remote monitoring with Node Exporter on other hosts

---


# Monitoramento com Grafana, Prometheus e Node Exporter

<div align="right">

  🇺🇸 [English version](#monitoring-with-grafana-prometheus-and-node-exporter)
</div>

---
Este projeto fornece um ambiente completo de monitoramento usando Docker Compose com:

- [Grafana](https://grafana.com/)
- [Prometheus](https://prometheus.io/)
- [Node Exporter](https://github.com/prometheus/node_exporter)

---

## 🚀 Como iniciar o projeto

### 1. Clone o repositório

```bash
git clone https://github.com/JPabloVM/infra-monitoring-kit.git
cd infra-monitoring-kit
```

### 2. Suba os containers

```bash
docker-compose up -d
```

> Isso criará e iniciará os serviços do Prometheus, Grafana e Node Exporter.

---

## 🔎 Acessos

- **Grafana**: [http://localhost:9091](http://localhost:9091)
  - Login: `admin`
  - Senha: `admin` (você será solicitado a alterar na primeira vez)

- **Prometheus**: [http://localhost:9095](http://localhost:9095)

- **Node Exporter**: [http://localhost:9100](http://localhost:9100)

---

## 🧠 Estrutura do projeto

```bash
.
├── docker-compose.yml
├── prometheus.yml                        # Configuração do Prometheus
└── grafana/
    └── provisioning/
        ├── datasources/
        │   └── prometheus.yml            # Fonte de dados do Grafana (Prometheus)
        └── dashboards/
            ├── dashboards.yml            # Provisionamento automático dos dashboards
            └── node-exporter-full.json   # Dashboard oficial do Node Exporter
```

---

## ✅ Primeiro acesso ao Grafana

1. Acesse o [Grafana](http://localhost:9091)
2. Faça login com `admin / admin`
3. Verifique se:
   - O **Data Source** chamado `DS_PROMETHEUS` foi criado
   - O **dashboard Node Exporter** aparece automaticamente no menu lateral
4. Pronto! O monitoramento já estará funcionando com dados em tempo real.

---

## ➕ Adicionando novos dashboards

1. Coloque o arquivo JSON do novo dashboard em:
   ```
   grafana/provisioning/dashboards/
   ```
2. Certifique-se de que o arquivo `dashboards.yml` já está apontando para essa pasta:
   ```yaml
   options:
     path: /var/lib/grafana/dashboards
   ```
3. Reinicie o container do Grafana:

   ```bash
   docker-compose restart grafana
   ```

> O novo dashboard será importado automaticamente.

---

## 🔌 Adicionando novos serviços a serem monitorados

1. Edite o arquivo `prometheus.yml`
2. Adicione uma nova `job_name` com os `targets` desejados. Exemplo:

   ```yaml
   scrape_configs:
     - job_name: 'meu-servico'
       static_configs:
         - targets: ['meu-servico:8080']
   ```

3. Reinicie o Prometheus:

   ```bash
   docker-compose restart prometheus
   ```

---

## 🧼 Resetando os dados

Para zerar completamente todos os dados (útil em desenvolvimento/testes):

```bash
docker-compose down -v
docker volume prune -f
```

---

## 📦 Requisitos

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose v2+](https://docs.docker.com/compose/)

---

## 🛠️ To-do / melhorias futuras

- Adicionar alertas configurados via Prometheus/Grafana
- Exportar dashboards como código versionado
- Monitoramento remoto via Node Exporter em outros hosts