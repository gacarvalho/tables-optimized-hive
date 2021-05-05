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

📢 ETAPA 4: VERIFICAÇÃO DA TABELA PARQUET

> Questão 4.1: Contar os registros da tabela pop_parquet
> Questão 4.2: Selecionar os 5 primeiros registros da tabela pop_parquet

O nosso objetivo agora é saber como está a consistência dos dados da tabela criada, para isso vamos realizar a primeira questão da Etapa 4. Utilizando a consulta ```select * from pop_parquet limit 5;``` é possível observar os dados perfeitamenete encaixados. 

![Verificacao da tabela parquet](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/5_6.%20Exericio_5_6_.png?raw=true)


📢 ETAPA 5: CRIANDO A TABELA COM A COMPRESSÃO DO TIPO SNAPPY

> Criar a tabela pop_parquet_snappy no formato parquet com compressão Snappy para ler os dados da tabela pop
> Inserir os dados da tabela pop na pop_parquet_snappy

Pronto, agora chegamos em uma parte interessante, o momento de criar a tabela com a compressão! Para isso vamos utilizar o comando ```create table pop_parquet_snappy(zip_code int, total_population int, median_age float, total_males int, total_females int, total_households int, average_households_size float) stored as parquet tblproperties('parquet.compress'='SNAPPY');```

E após a criação, vamos analisar a descrição dessa tabela com o comando desc formatted pop_parquet_snappy; Como é possível observar na imagem abaixo, a linha selecionada mostra que os parâmetros da tabela tem um parquet do tipo compressão SNAPPY.
![CRIANDO A TABELA COM A COMPRESSÃO DO TIPO SNAPPY](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/7_8.%20Exercicio_7_8_.png?raw=true)

📢 ETAPA 6: VERIFICANDO A CONSISTÊNCIA DA TABELA pop_parquet_snappy

> Contar os registros da tabela pop_parquet_snappy
> Selecionar os 5 primeiros registros da tabela pop_parquet_snappy

Agora na etapa 6, vamos verificar a consistência da tabela pop_parquet_snappy contando o número de registros da tabela com o comando ```select count(*) from pop_parquet_snappy;```

E logo após verificar o número de registros na tabela. Para isso, vamos selecionar os primeiros 5 registros!
![VERIFICANDO A CONSISTÊNCIA DA TABELA pop_parquet_snappy](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/9_10.%20Exercicio_9_10_.png?raw=true)

📢 ETAPA 7: COMPARANDO AS TABELAS

> Comparar as tabelas pop, pop_parquet e pop_parquet_snappy no HDFS. 
 
Para realizar a etapa 7 vamos comparar as tabelas, verificando a consistência de cada uma e analisando o conteúdo. Antes de mais nada, vamos consultar as tabelas que estão presentes no nosso Hive com o comando ```hdfs dfs -ls /user/hive/warehouse/empresastartup.db```. É fácil observar as tabelas (1) pop (2) pop_parquet (3) pop_parquet_snappy.
![COMPARANDO AS TABELAS](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/11_a.%20Mostrando%20as%20tabelas%20internas%20no%20hive.png?raw=true)

Para verificar os dados e o seus tamanhos, vamos utilizar o comando hdfs dfs -du -h
/user/hive/warehouse/empresastartup.db
![COMPARANDO AS TABELAS](https://github.com/gacarvalho/criacao-tabelas-otimizadas/blob/main/Cria%C3%A7%C3%A3o%20de%20Tabelas%20Otimizadas/11_b.%20Exercicio_11.png?raw=true)
