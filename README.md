# Relatório de Implementação e Otimizações - Desafio Kubernetes com Prometheus e Grafana

## Procedimentos e Análises

Inicialmente, a infraestrutura foi configurada usando um cluster Kubernetes com três nós (um master e dois workers), utilizando k3s. A configuração do cluster k3s foi realizada via Ansible, com o script automatizando a obtenção do token necessário para os workers se conectarem ao master. Após a execução do playbook, tanto o cluster master quanto os workers já estavam em pleno funcionamento, prontos para receber as aplicações e serviços.

O Prometheus e o Grafana foram implantados como parte do monitoramento do ambiente. Durante o processo, foram configurados serviços com NodePort para expor ambas as ferramentas e garantir acessibilidade externa. Além disso, foi necessário ajustar os manifests de deployment para garantir volumes persistentes no Grafana.

## Modificações Realizadas

- **Prometheus**: Inicialmente, o serviço estava configurado como ClusterIP, dificultando o acesso externo. Foi alterado para NodePort, permitindo acessibilidade externa.
- **Grafana**: Volumes foram adicionados para persistir dados e manter configurações entre recriações de pods. Isso otimiza a continuidade das operações em caso de reinicialização.
- **Dockerfile**: Implementado o build da aplicação via GitHub Actions e configurado o envio da imagem para o Docker Hub devido a problemas de autenticação com o GitHub Container Registry (GHCR).
- **Pipeline CI/CD**: A pipeline foi configurada para construir a imagem da aplicação e realizar o deploy em um cluster Kubernetes. O Docker Hub foi utilizado para o armazenamento da imagem, e ajustes serão feitos para alterar a imagem para um repositório privado e resolver o problema de autenticação para futuras melhorias.

## Dificuldades Iniciais

Uma das maiores dificuldades enfrentadas foi o fato de não ter trabalhado previamente com Kubernetes. O processo de mapeamento dos nós foi desafiador, especialmente para garantir que os nós do cluster fossem identificados corretamente e atribuídos para a execução das funções desejadas (master e workers). Além disso, o uso do NodePort para expor a aplicação fora dos pods foi essencial para garantir acessibilidade externa, mas apresentou algumas dificuldades iniciais no mapeamento correto de portas e IPs no ambiente distribuído.

## Otimizações

- A utilização de NodePort foi uma escolha rápida para acesso externo, mas em produção recomenda-se a implementação de um Ingress controlado por certificados TLS.
- A pipeline CI/CD foi otimizada para incluir a autenticação automática com o registro de contêineres, evitando falhas de permissão.
- Outra recomendação é otimizar a imagem da aplicação, que atualmente está utilizando o Node.js 20. O build está demorando cerca de 5 minutos para rodar, o que pode ser reduzido ao utilizar versões menores ou ajustes no cache do Docker.

## Avaliação do Desafio

### Dificuldades

Houveram problemas iniciais com autenticação no GitHub Container Registry (GHCR) devido à configuração inadequada do token. Além disso, o mapeamento correto entre o Prometheus e as métricas da aplicação exigiu ajustes finos no arquivo de configuração. A falta de experiência com Kubernetes foi um dificultador adicional, tornando o mapeamento de nós e a configuração do ambiente distribuído mais desafiadores.

### Tempo de Execução

A implementação total levou aproximadamente 10 horas, incluindo a correção dos problemas de autenticação, ajustes na pipeline e testes de conectividade entre os serviços do cluster.

### Implementações Adicionais

Foi adicionada a integração do Prometheus para monitorar métricas customizadas da aplicação e configuração de volumes persistentes no Grafana.

## Conclusão e Status Atual

O ambiente está operacional com Prometheus, Grafana e a aplicação rodando de forma estável no cluster Kubernetes. As métricas estão sendo coletadas corretamente e o monitoramento foi implementado com sucesso.

## Recomendações Finais

- Implementar um Ingress Controller para gerenciar o tráfego de entrada com certificados SSL.
- Habilitar autenticação no Grafana para garantir a segurança do acesso.
- Realizar testes de carga para garantir que o cluster suporte o tráfego esperado em produção.
- Otimizar a imagem Docker da aplicação, pois o build está levando cerca de 5 minutos. Avaliar o uso de uma versão menor do Node.js ou melhorar o uso de cache para reduzir o tempo de build.
