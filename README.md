# kubernetes-elastic-logging

Esta é uma configuração de exemplo para o log automatizado com a pilha elástica no Kubernetes.

### Visão Geral:

- Elasticsearch para armazenar e pesquisar logs.
- Kibana por vê-los.
- Logstash para analisar e dividir logs.
- Logbeat de arquivo para enviar todos os logs do aplicativo para o logstash.
- Metricbeat para enviar a análise do host para o  elasticsearch.
- Curador para excluir regularmente registros antigos.


O Elasticsearch é instalado como um StatefulSet para que haja alguma
consistência entre eles.


As instâncias Filebeat e Metricbeat são instaladas como DaemonSets,
ou seja, existe um para cada nó que temos. Isso é porque eles
leia os logs diretamente do nó. Sem isso, perderíamos logs
de alguns nós.



### Instalação:
- Atualize primeiro o arquivo kibana-deployment.yaml para que a entrada / rota corresponda a uma que aponta no seu cluster.
- Para instalar isso em um cluster, aplique todos os arquivos.
 - É mais seguro fazer os arquivos de elasticsearch primeiro e aguardar o pods para iniciar. Lembrand que  o pod logstash falhará se não puder se conectar ao elasticsearch (reiniciando).
- No restante, não importa a ordem.


Se você quer viver perigosamente, basta aplicar o diretório raiz:

```kubectl apply -f kubernetes-elastic-logging```
        




Baseado inicialmente no projeto https://gitlab.com/ndevox/kubernetes-elastic-logging/tree/master
