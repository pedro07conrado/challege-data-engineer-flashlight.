# Data Pipeline com Apache Airflow
#### Desafio de Código - Tech Indicium
#### Desenvolvido por Pedro Conrado Negreiro da Silva

## Visão Geral
Este projeto foi desenvolvido como parte do desafio de código da Tech Indicium. O objetivo é criar um pipeline de dados usando Apache [Airflow]([url](https://airflow.apache.org/)) para extrair dados de duas fontes distintas, armazenando os dados no disco local e, em seguida, gravando em um banco de dados.

![diagrama_embulk_meltano (1)](https://github.com/pedro07conrado/challege-data-engineer-flashlight./assets/113401454/fd6d1f64-0cfe-4c59-a356-7d78c2469ff1)





# Tecnologias Utilizadas
<p align="center">
   <img src="https://raw.githubusercontent.com/github/explore/main/topics/python/python.png" alt="Python" width="70" height="70"/> 
   <img src="https://raw.githubusercontent.com/github/explore/main/topics/postgresql/postgresql.png" alt="PostgreSQL" width="60" height="60"/>
   <img src="https://upload.wikimedia.org/wikipedia/commons/d/de/AirflowLogo.png" alt="Airflow" width="85" height="60"/> 
</p>

- Apache Airflow 2.9.1. 
- Python 3.10.12. 
- PostgreSQL. 

### Estrutura do Projeto
airflow/ \
├── dags/ \
│   └── dag_extracao_daily.py (Definição do DAG) \
├── data/ \
│   ├── csv/ \
│   │   └── order_details.csv (Arquivo CSV de entrada) \
│   ├── postgres/ (Diretório para dados extraídos do PostgreSQL) \
│   └── output/ (Diretório para dados transformados e salvos) 

### Estrutura do DAG
#### O DAG é composta por três tarefas principais:

- **Extração de Dados do PostgreSQL**: 
Conecta ao banco de dados PostgreSQL e extrai dados das tabelas especificadas. \
Salva os dados extraídos como arquivos CSV no diretório airflow/data/postgres.

- **Extração de Dados do CSV**

- **Transformação e Salvamento de Dados:**
Lê os dados extraídos do PostgreSQL e do arquivo CSV. \
Realiza transformações nos dados, como a junção de tabelas.

# Instalação
#### 1. Clone o repositório:
git clone:
```
git@github.com:pedro07conrado/challege-data-engineer-flashlight.git
``` 
`cd <seu-repositorio>`

#### 2. Configurar o ambiente virtual:
```
python3.10 -m venv venv 
source venv/bin/activate
```

#### 3. Instalar as dependências:
```
pip install apache-airflow==2.9.1 
pip install psycopg2 pandas
```

#### 4. Configurar o PostgreSQL:
Certifique-se de ter um banco de dados PostgreSQL em execução. \ 
Atualize as credenciais de conexão no script dag_extracao_daily.py.

#### Configuração do Airflow
##### Inicializar o banco de dados do Airflow: 
```
airflow db init
```

#### Criar um usuário administrador: 
- airflow users create 
- username: admin 
- firstname: Pedro 
- lastname: Silva 
- role: Admin 
- email seu-email@example.com
   

### O Airflow fornece um serviço web para monitorar e solucionar problemas em pipelines. Para iniciar o servidor web:
 ```
airflow webserver -p 8080
```
Então no seu navegador acesse [localhost](http://localhost:8080/home) para visualizar o seu pipeline

# Problemas e Soluções

### Problema: Configuração do PostgreSQL no Linux Mint

> [!IMPORTANT]
> Tive problemas para executar o PostgreSQL usando o dual boot no Linux Mint. A configuração padrão não funcionou conforme esperado.

**Solução:**
> O vídeo [How to Install PostgreSQL on Linux Mint](https://www.youtube.com/watch?v=BykmBY-GgvE&t=1s) foi extremamente útil para resolver esses problemas. 
> Seguindo os passos, consegui instalar e configurar corretamente o PostgreSQL. 
>
> - Certifique-se de que todos os pacotes estejam atualizados:
>
> ```bash
> sudo apt update && sudo apt upgrade
> ```
>
> - Após isso, siga o tutorial do vídeo para os detalhes da instalação.

---

### Problema: Conflito de PID no Airflow

> [!IMPORTANT]
> Ao tentar iniciar o Airflow, enfrentei conflitos com o PID, o que impedia sua execução correta.

**Solução:**
> Identifiquei o processo em conflito utilizando o comando:
> 
> ```bash
> ps aux | grep airflow
> ```
> 
> Depois finalizei o processo em conflito com:
> 
> ```bash
> kill <pid>
> ```
> 
> Onde `<pid>` deve ser substituído pelo número do processo listado.
