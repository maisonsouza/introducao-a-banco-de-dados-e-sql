# Curso de MySQL I: Iniciando suas consultas

## Consultando os dados
```
SQL - Linguagem de Banco de Dados
Banco de dados do curso: Mysql (Gratuito).
Utilizaremos o console.
```

#### Comando para entrar no banco de dados Mysql
```
Abrir o CMD do Windows
mysql -u root -p
senha: **************
```

#### Criar um banco de dados
```
create database controle_compras;
```
 
#### Verificando os bancos de dados existentes
```
show databases;
```
> Nota: Todo comando sql termina com ;(ponto-e-virgula).
 
#### Selecionando o banco de dados
```
use controle_compras;
```

#### Criando tabelas no banco criado
```
create table compras (id int auto_increment primary key, valor double, data date, recebido boolean, observacoes varchar (255));
```
 
#### Verificar a estrutura da tabela
```
desc compras; 
```

#### Verificar o código de criação da tabela
```
show create table compras;
```

#### Inserindo dados na tabela.
```
insert into compras (valor, data, recebido, observacoes) values (1000, '2019-06-08',1,'Conjunto de cadeiras');
```

#### Selecionando todos os dados de uma tabela
```
select * from compras;
```

#### Selecionando a tabela com as colunas
```
select observacoes, data, valor from compras;
```

#### Trabalhando com filtros (Where)
```
select * from compras where valor > 1000;
```
> Nota: Seta pra cima mostra últimos comandos.

#### Mais de um filtro com and
```
select * from compras where valor < 1000.00 and recebido =1;
```
> Nota: Para casas decimais utilize .

#### Mais de um filtro com or
```
select * from compras where valor <100 or recebido=0;
```

#### Mais de um filtro com diferente
```
select * from compras where recebido <> '0';
```

#### Filtro em palavras com like
```
select * from compras where observacoes like '%a%';
```
> Nota: Não existe diferença de usar aspas simples e aspas duplas.

## Atualizando e excluindo dados
#### Utilizando o Between
```
select * from compras where valor between 200 and 700;
select * from compras where data between '2009-01-01' and '2010-01-01';
```

#### Alterando um valor da tabela
```
update compras set valor = 900 where id =20;
```
#### Deletando uma linha da tabela
```
delete from compras where id = 41;
```

## Alterando e restringindo o formato das nossas tabelas
#### Alterando os parametros da tabela
```
alter table compras modify observacoes varchar (255) not null;
alter table compras modify recebido tinyint(1) default '0';
```

#### Adicionando colunas na tabela já criada
```
alter table compras add column forma_pagto enum ('cartao', 'boleto', 'dinheiro');
```
```
 Nota - not null impede que o campo seja null
 Default - configura um valor padrão para o campo
 Enum (um tipo que configura entrada padrão para o campo)
```

## Agrupando dados e fazendo consultas mais inteligentes
#### Somando os campos de uma coluna com funções de agregaçao
```
select sum(valor) from compras;
```

#### Contando os campos de uma coluna com funções de agregação
```
select count(valor) from compras;
```

#### Nomeando o titulo da coluna
```
select sum(valor) as Soma, count(valor) as Quantidade from compras;
```

#### Tirando a média dos campos de uma coluna
```
select month(data),year(data),avg(valor) as media from compras group by month(data), year(data);
```
> Para agrupar as consultas que utilizam funções de agregação precisamos do group by
> Para ordenar o resultado por critérios utilizanos o order by

#### Alterando o nome de uma coluna da tabela
```
alter table compras change column forma_pagto forma_pagt enum ('boleto', 'cartao', 'dinheiro');
```

## Juntando dados de várias tabelas 
#### com inner join (chave primaria = chave estrengeira)
```
select nome, sum(valor) from compras 
inner join compradores on compras.comprador_id = compradores.id
group by nome;
```

#### Adicionando a chave estrangeira
```
alter table add foreign key (comprador_id) references compradores(id);
```
