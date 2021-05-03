## CRIAÇÃO DE TABELAS OTIMIZADAS 🗜

O objetivo do projeto é trabalhar com a criação de tabelas otimizadas utilizando o framework Hive em conjunto com HDFS. Vale lembrar que, para execução do ambiente, estamos utilizando o docker. 

---

📢 ETAPA 1: INICIANDO OS SERVIÇOS

O primeiro passo do projeto é iniciar os serviços, subindo alguns frameworks com auxilio do docker, para isso vamos aplicar o comando ```docker-compose up -d```. Como é possível analisar, todos os serviços estão disponíveis. 

![Iniciando dos servicos](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/Iniciando%20os%20servicos%20docker.png?raw=true)

Depois de iniciar os serviços, vamos utilizar a base de dados e exibir as tabelas do DB, e podemos ver isso na figura abaixo.

![ Mostrando os DB](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/Exercicio_1_.png?raw=true)

📢 ETAPA 2: VERIFICAR A DISPONIBILIDADE DOS DADOS

>  Questão 2.1: Selecionar os 10 primeiros registros da tabela pop

Para quem trabalha com dados, sabe da importância de verificar a disponibilidade dos dados. Para aplicarmos a etapa 2, vamos realizar a seguinte consulta ```select * from pop 10;```. Na figura  abaixo está evidente a presença dos dados na tabela pop. 

![Disponibilidade dos dados](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/2.%20Exericio_2_.png?raw=true)

📢 ETAPA 3: CRIAÇÃO DA TABELA PARQUET

> Questão 3.1: Criar a tabela pop_parquet no formato parquet para ler os dados da tabela pop
> Questão 3.2: Inserir os dados da tabela pop na pop_parquet

Agora vamos criar uma tabela no formato parquet. O que é Parquet? É possível entender Parquet como um formato de armazenamento baseado em coluna para o Hadoop. 

Para isso, vamos aplicar o código ```create table  pop_parquet(zip_code, total_population int, median_age float, total_males int, total_females int, total_households int, average_households_size float) stored as parquet```

Vale lembrar que vamos transferir os dados da tabela pop para a tabela pop_parquet com a consulta ``` insert into pop_parquet select * from pop;```

![Criacao da tabela parquet](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/3_4.%20Exercicio_3_e_4_.png?raw=true)
