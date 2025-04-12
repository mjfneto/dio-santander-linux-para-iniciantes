# Docker: Utilização Prática no Cenário de Microsserviços

## Migrar para uma nuvem pública

Aplicações em _bare metal_, instaladas diretamente em servidores, em nuvem local (e.g. data center).

### "Problemas" da nuvem privada

1. Dificuldades com a segurança da Tecnologia da Informação (lógica e física);
2. Custo com mão de obra especializada;
3. Custo de Hardware;
4. Custo de energia elétrica;
5. Falta de energia (uso de geradores);
6. Despesas inesperadas.

### Vantagens da nuvem pública

1. Preço (pague somente o que usar);
2. Facilidade de contratação, configuração e infraestrutura;
3. Escalabilidade;
4. Performance.

---

> **(Gemini 2.0 Flash)**
>
> Os principais players de serviços de nuvem pública hoje (12/04/2025) são:
>
> - **Amazon Web Services (AWS):** Líder de mercado, oferece um conjunto vasto e abrangente de serviços de nuvem, desde computação e armazenamento até inteligência artificial e machine learning. Possui a maior participação de mercado e uma vasta gama de serviços maduros.
> - **Microsoft Azure:** O segundo maior player, conhecido por sua forte integração com o ecossistema Microsoft e soluções híbridas. Apresenta um crescimento significativo e uma ampla gama de serviços, incluindo IA e suporte para ferramentas Microsoft.
> - **Google Cloud Platform (GCP):** Focado em inovação em áreas como inteligência artificial, machine learning, análise de dados e Kubernetes. Tem ganhado popularidade, especialmente entre empresas que utilizam os serviços do Google.
> - **Alibaba Cloud:** Líder no mercado asiático, oferece uma gama completa de serviços de nuvem e possui forte presença na região da Ásia-Pacífico.
> - **Oracle Cloud Infrastructure (OCI):** Destaca-se por sua oferta para cargas de trabalho empresariais, especialmente aquelas que envolvem bancos de dados Oracle, e por seu suporte a ambientes híbridos.
> - **IBM Cloud:** Focado em soluções de nuvem híbrida e multi-cloud, aproveitando sua expertise em mainframe e serviços de consultoria.
> - **Tencent Cloud:** Outro player importante na Ásia, com forte presença na China.
> - **Huawei Cloud:** Uma provedora de nuvem em crescimento, com investimentos significativos em infraestrutura e serviços.
>
> De acordo com o Gartner Magic Quadrant para Strategic Cloud Platform Services de 2024, AWS, Microsoft e Google são considerados Líderes, demonstrando visão completa e capacidade de execução no mercado de nuvem pública.

## Microsserviços

Microsserviços são um tipo inovador de arquitetura de software, que consiste em construir aplicações desmembrando-as em serviços independentes. Estes serviços se comunicam entre si usando APIs (usando normalmente JSON) e promovem grande agilidade em times de desenvolvimento.

Hoje, gigantes do mercado, como Netflix e Spotify, divulgam a receita do sucesso ao transformar suas aplicações monolíticas em mais de 500 microsserviços.

Quando quebramos uma aplicação monolítica em várias pequenas partes, conseguimos escalá-las de forma separada. Supondo que um serviço de autenticação seja chamado várias vezes durante a sessão de um usuário, com certeza o estresse sobre ele é maior.

Com microsserviços, podemos escalar apenas uma parte, ao invés de ter que escalar a aplicação como um todo, como ocorre em uma arquitetura monolítica.

Os microsserviços não necessariamente precisam ser escritos usando a mesma linguagem de programação.

## O que é um Cluster e Docker Swarm?

Um **_cluster_** (inglês: grupo, aglomerado) consiste em computadores ligados que trabalham em conjunto, de modo que, em muitos aspectos, podem ser considerados, como um único sistema. Computadores em cluster executam a mesma tarefa, controlados e programados por software. Cada computador presente em um cluster é conhecido como **_node_** (nó).

### O que é Docker Swarm?

O **_swarm_** é um recurso do Docker que fornece funcionalidades de orquestração de contêiner, incluindo clustering nativo de hosts do Docker e agendamento de cargas de trabalho de contêineres. Um grupo de hosts do Docker forma um cluster "Swarm".

> Uma vantagem de um swarm é que, no caso de falha em um dos nodes, as tarefas são automaticamente passadas para outros.

## Entendendo as definições do primeiro container

- [MySQL — Docker Hub](https://hub.docker.com/_/mysql)

## Criando um container MySQL

## Estressando o container

- [loader.io](https://loader.io/)

## Iniciando um cluster Swarm

## Criando um serviço no cluster

## Replicando um volume dentro do cluster

## Criando um proxy utilizando o NGINX

## Estressando o cluster
