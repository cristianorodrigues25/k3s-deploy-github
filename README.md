# README

## Visão Geral

Este projeto é uma aplicação baseada em Kubernetes, que utiliza Grafana para visualização de métricas e Prometheus para coleta de métricas. A infraestrutura é configurada para suportar alta disponibilidade e escalabilidade, e inclui os seguintes componentes principais:

- **Kubernetes Cluster**: Gerencia a execução e o escalonamento dos containers.
- **Grafana**: Utilizado para visualização de métricas e criação de dashboards.
- **Prometheus**: Coleta e armazena métricas para visualização no Grafana.
- **Aplicação Coffee Shop**: Aplicação web disponível para acesso.

## Estrutura da Infraestrutura

### Kubernetes Cluster

O projeto está executando um cluster Kubernetes, que inclui:

- **3 Nós**:
  - `cluster-1-node-01`: Master node e também um worker node.
  - `cluster-1-node-02`: Worker node.
  - `cluster-1-node-03`: Worker node.

### Aplicação Coffee Shop

A aplicação Coffee Shop está disponível para acesso via web.

- **Endereço**: [http://34.94.136.0:30000/](http://34.94.136.0:30000/)

### Grafana

Grafana é configurado para monitorar e visualizar métricas. 

- **Endereço**: [http://34.94.136.0:32000/](http://34.94.136.0:32000/)

### Prometheus

Prometheus é utilizado para coleta de métricas, que são visualizadas no Grafana.

- **Endereço**: [http://34.94.136.0:31090/](http://34.94.136.0:31090/)

