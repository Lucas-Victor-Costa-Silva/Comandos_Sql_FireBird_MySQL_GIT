 <h1>Comandos FireBird, MySQL, Git</h1>

## Índice

* FireBird: linha   10  até  411
* MySql:    linha   415 até  635  
* Git:      linha   637 até  700  
* Tortoise: linha   702 até  702

## Comando Básicos de Firebird 

<p>para abrir o terminal , pesquise na lupa no windows : firebird, 
para fechar o terminal : quit ;</p>

<h3>conexção com o servidor  do firebird</h3>
<p>connect 'C:\Users\SAMSUNG\Desktop\FB\EX03.FDB' user 'SYSDBA' password 'masterkey';</p>

## Criando uma Banco de dados no Firebird

<p>create database 'C:\Users\SAMSUNG\Desktop\FB\EX03.FDB' user 'SYSDBA' password 'masterkey';</P>

## Criando uma tabela no Firebird

<p>CREATE TABLE clientes  (
id  INTEGER NOT NULL ,
nome VARCHAR (30)
);

ou usando domínios :

CREATE TABLE CLIENTES (
nome DM_NOME,
codigo DM_CODIGO
);</p>

## APAGANDO UMA TABELA

<p>DROP TABLE CLIENTES;</p>

## Comando   para  ver as tabelas criadas

<p>show table; 

para ver as colunas de uma tabela específica , basta digitar o nome da tabela (OBS: usando uma tabela como exemplo chamada:  clientes) :

show table clientes ;</p>

## COMANDO DE INSERIR REGISTRO NA TABELA                                                         

<p>INSERT INTO clientes VALUES
(1,'Lucas'); 
COMMIT;</p>

## APAGANDO REGISTRO DE UMA TABELA

<p>DELETE FROM  CLIENTES  
WHERE ID = '1';

OU APAGA TUDO :

DELETE FROM CLIENTES;</p>

## CRIANDO UM DOMÍNIO 

<p>CREATE DOMAIN "DM_NOME" VARCHAR (20) NOT NULL;   <em><- não pode colocar CONSTRAINT</em></p>

## APAGANDO UM DOMÍNIO

<p>DROP DOMAIN "DM_NOME";</p>

## CRIAR DOMAIN

<p>CREATE DOMAIN DMN_NAO_SIM AS
CHAR(1) CHARACTER SET WIN1252
NOT NULL
CHECK (VALUE IN ('S', 'N'))
COLLATE WIN_PTBR;

CREATE DOMAIN DMN_NAO_SIM AS
CHAR(1) CHARACTER SET WIN1252
NOT NULL
CHECK (VALUE IN ('S', 'N'))
COLLATE WIN_PTBR;

CREATE DOMAIN DMN_FISICA_JURIDICA AS
CHAR(1) CHARACTER SET WIN1252
NOT NULL
CHECK (VALUE IN ('FISICA', 'JURIDICA'))
COLLATE WIN_PTBR;</p>

## CRIANDO UMA COLUNA

<p>ALTER TABLE PRODUTOS
 ADD NOME VARCHAR (20) NOT NULL;</p>

## APAGANDO UMA COLUNA

 <p>ALTER TABLE PRODUTOS 
DROP CODIGO;<p>

## MODIFICANDO UM TAMANHO DE UMA COLUNA

<em>OBS: O comando  não será aceito se o novo tamanho for menor que o tamanho atual</em>

<p>alter table CURSOS
alter NOME type varchar (30);</p>

**** ALTERANDO UM NOME DE UM CAMPO ****

ALTER TABLE CURSOS
ALTER DESCRITION TO DESCRICAO;    --------> INFORMAR QUAL É O NOME ANTIGO ANTES

**** ALTERANDO O TYPO DE UM CAMPO  DA TABELA ****

ALTER TABLE TBLEPG ALTER COLUMN SEXPES TYPE DMN_SEXO;
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** ADICIONADO UMA CHAVE  PRIMÁRIA ****

ALTER TABLE PRODUTOS
ADD CONSTRAINT PK_CODIGO        --------> nome da sua chave primária 
PRIMARY KEY (CODIGO);

**** APAGANDO UMA CHAVE PRIMÁRIA OU CHAVE ESTRANGEIRA ****

ALTER TABLE PRODUTOS
DROP CONSTRAINT PK_CODIGO ;
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** ADICIONANDO UMA CHAVE ESTRANGEIRA A OUTRA TABELA **** 

ALTER TABLE PRODUTO 
ADD CONSTRAINT FK_PRO_GRUPO 
FOREIGN KEY (PRO_GRUPO)
REFERENCES  GRUPO(GRU_ID);         --------> NÃO DEIXE ESPAÇOS , DEIXE JUNTOS

**** APAGANDO UMA CHAVE ESTRANGEIRA ****

ALTER TABLE CLIENTES 
DROP CONSTRAINT FK_PRO_GRUPO;     --------> NOME DA CONSTRAINT

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** COMANDO UPDATE ****

UPDATE  CLIENTES
SET  CLIENTES.NOME = 'RAINHA'     --------> PARA  ALTERAR UM CAMPO DO REGISTRO;
WHERE  CLIENTES.ID = '3';

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

*************** SELECT ***************

DQL

SELECT * FROM CURSOS ;     --------> mostra todos os registros da sua tabela

SELECT  nome , ano FROM  cursos
WHERE  ano = '2020'                -------->  filtrar por linha
ORDER BY  nome DESC ;    --------> mostra o nome , ano , quando os registros forem do ano 2020  e vai ser ordernado  por nome descrecente.

SELECT ano , nome FROM cursos     -------->  filtra por coluna
ORDER BY  ano, nome;

podemos usar operadores relacionais no whare também : = , < , > , !=  <> , <=, >= 

SELECT  nome , profissao FROM cursos
WHERE  nascimento >=  '2022' 
ORDER BY nome;


outros operadores :


* between  significa filtra  um número x até y

select  ano , nome from cursos
where ano between '2000' and '2025' ;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
* in  significa filtra número  x e y e g 

select ano , nome from cursos
where ano in ('2000' , '2015' , '2021')
order by ano , nome;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

*Eu posso combinar os dois 

selec * from cursos
where carga < 30 and totaulas > 20 ;     ----> aperadores lógicos:  and = e , or = ou , not = não 


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
* Filtra registros com as letras parecida ou palavras que começa com determinada letra :  like 

select  *  from cursos
where nome like 'P%' ;


ou eu posso fazer o inverso , filtrar regitros com letrar terminadas com x letras 

select nome from cursos
where nome like '%A' ;  

ou eu posso fazer os dois juntos , obs: essa porcentagem significa carta coringa e ela pode ter qualquer valor ou nenhum : 

select nome from cursos
where nome like '%a%' ;     --------> pode aparecer Amanda , porque o curinga pode ter qualquer letra e essa condição se encaixa nesse requisito.

% = _   essas são as duas cartas curingas , a diferença é que o _ obriga a ter pelo o menos um  character o % pode ser uma character ou nada , numeros atende os dois também.


* o outros comando do select:

select max(altura) from pessoas;   --------> vai  selecionar a maior altura 

selec min(altura) from pessoas;    --------> vai  selecionar a menor  altura 

select count(nomes) from pessoas;  --------> vai contar quantos nomes que tem na tabela

select sum(anos) from cursos;      --------> vai somar os anos da tabela cursos ;

select distinct nacionalidade from pessoas 
order by nacionalidade;  --> vai filtra as nacionalidades e não vai mostrar as nacionalidades repetidas. Com o 'order by nacionalidade' vai colocar de ordem alfabética.

select nacionalidade, count(*) from pessoas
group by nacionalidade  ;  --> vai fazer um agrupamento de nacionalidade sendo que são iguais ou difetentes e também com o comando count() podemos saber quantas nacionalidade tem cada grupo ,detro do count() pode ter qualquer coluna.

select avg(salario) from funcionarios 
where sexo = 'F' ;   --> esse avg significa a média , no caso do where  ele é uma condição para que a média seja calculadas dos sálarios das mulheres;


SELECT * FROM clientes ;  -------->  para  mostrar os registros da tabela 

SELECT PRODUTO.PRO_ID FROM PRODUTO
WHERE PRODUTO.PRO_ID >= 1 AND PRODUTO.PRO_ID <= 5 ;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** COMANDOS JOINS ****


*JUNTANDO DUAS TABELAS COM O JOIN = INNER JOIN:

SELECT * FROM PRODUTO 
JOIN GRUPO 
ON PRODUTO.PRO_GRUPO = GRUPO.GRU_ID ;  -------->  ON OBRIGATÓRIO  PARA NÃO DUPLICAR   OS REGISTROS                                                            

*DANDO PRIORIDADE PARA A TABELA  À ESQUERDA AO JOIN: 

SELECT * FROM PRODUTO 
LEFT JOIN GRUPO
ON PRODUTO.PRO_GRUPO = GRUPO.GRU_ID ;

*DANDO PRIORIDADE PARA A TABELA  À  DIREIRA AO JOIN:

SELECT * FROM PRODUTO 
RIGHT JOIN GRUPO 
ON PRODUTO.PRO_GRUPO = GRUPO.GRU_ID ;

*EU POSSO DAR APELIDO PARA A MINHAS TABELAS :

SELECT CLI.NOME , CUR.NOME , CUR.ANO
 FROM CLIENTES AS CLI 
INNER JOIN CURSOS AS CUR 
ON CUR.ID = CLI.CURSO_PREFERIDO; 

*SEM APELIDOS :

SELECT CLIENTES.NOME , CURSOS.NOME , CURSOS.ANO 
FROM CLIENTES INNER JOIN CURSOS 
ON CURSOS.ID = CLIENTES.CURSO_PREFERIDO;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** Cardinalidade  de banco de dados ****

O primeiro passo é  identifiacar qual é o relacionamento de entidades exemplos:
 1 para  1      ou      1 para  n       ou   n para n 
1 para 1  : a chave primaria do dominada vai ser enviada para o dominante e assim vai surgir o conceito de chave estrangeita (EXEMPLO) :     Marido  recebe chave primária  de Esposa  
1 para n  :   em regra  pega a chave primária de 1 e  manda para n :  Pai manda a chave primária para os seus filhos.

n para n :  nesse contexto vai surgir mais uma entidade , e vai seguir a regra de 1 para n :
pessoa 1      n compra n    1 produto 
Depois disso segue a regra de 1 para n 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
****Exercícios select****


1) Faça uma lista com o nome de todas as mulheres.

R- select nome from pessoas
   where sexo = 'F';

2) Faça uma lista com os dados de todos aqueles que nasceram entre  01/Jan/2000 e 31/Dez/2015.

R- select * from pessoas
   where ano between '2000' and '2015' ;

3) Faça uma lista com o nome de todos os homens que trabalham como Programadores.

R- select nome from pessoas 
   where sexo = 'M' and profissao = 'Programadores';

4) Faça uma lista com os dados de todas as mulheres que nasceram no Brasil e que têm seu nome iniciando com a letra J.

R- select * from pessoas
   where sexo = 'F' and nacionalidade = 'Brasil' and nome like 'J%';

5) Faça uma lista com o nome e nacionalidade de todos os homens que têm Silva no nome, não nasceram no Brasil e pesam menos de 100 KG.

R - select nome , nacionalidade from pessoas
    where sexo = 'M' and nome like '&_Silva&' and not nacionalidade 'Brasil' and peso > 100;

6) Faça uma lista que mostra qual é a maior altura entre os homens que moram no Brasil.

R- select max(altura) from pessoas
   where sexo = 'M' and nacionalidade 'Brasil';

7) Faça uma lista que mostra qual é o menor peso entre as meninas que nasceram fora do Brasil e entre 01/01/1990 e 31/12/2000.

R - select min(peso) from pessoas
    where sexo = 'F' and nacionalidade != 'Brasil' and nascimento between '1990' and '2000';

8) Faça uma lista que mostra quantas mulheres têm mais de 1.90m.

R- select count(altura) from pessoas
   where sexo = 'F' and altura > '1.90'

*****Exercícios de select usando agrupamentos*******

1) Faça uma lista com as profissões dos meninos e seus respectivos quantitativos.

R- select profissao , count(*) from pessoas
   where sexo = 'M'
   group by profissao;

2) Faça uma lista que mostre quantos homens e mulheres nasceram após 01/01/2005

R - select count(*) from pessoas
    group by sexo
    having (select count(*) from pessoas where nascimento >=  '2005'  );

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** GENERATOR INCREMENT/TRIGGER PARA CHAMAR ESSE GENERATOR ****

create generator INc_Produto ;
set generator INc_Produto to  9;  --------> ESSE NOVE REPRESENTA O SEU ÚLTIMO  NÚMRO DO CAMPO ID, VOCÊ QUE ESCOLHE , E VOCÊ ESCOLHE O NOME

set term ^ ;     --------> no ibexpert não precisa colocar essa linha
create trigger PRODUTO_BI for PRODUTO    --------> PRODUTO_BI  significa :  B before , I  insert 
active before insert position 0          --------> FOR  PRODUTO  significa : da tabela  Produto
as
begin
  if (new.PRO_ID is null) then
     new.PRO_ID = gen_id (INC_PRODUTO ,1);       --------> GEN_ID significa o  GENERATOR 
end^            --------> no ibexpert não precisa colocar esse '^'  sinal
set term ; ^    --------> no ibexpert não precisa colocar essa linha

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** EXCEÇÃO/TRIGGER PARA CHAMAR ESSA EXCEÇÃO ****

CREATE  EXCEPTION  EXC_CLIENTES ('NÃO POSSO APAGAR ESSE CLIENTE');

set term ^;   <- no ibexpert não precisa colocar essa linha

create trigger Exc_ClinteBD for CLIENTES
active before delete position 0
as
begin
  if (old.ID = 1) then
  exception EXC_CLIENTES;
end^    <- no ibexpert não precisa colocar esse '^'  sinal

set term ; ^   <- no ibexpert não precisa colocar essa linha

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** APAGANDO UMA TRIGGER ****

DROP TRIGGER TRG_TBLEPG;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** procedures ****

create procedure calc_comissao
(servico_indicado float , seu_salario float )         -------->input
returns (Bonus_comissao float , salario_final float)  --------> output
as
declare variable  p float;     --------> assim que declara uma variável (local)
begin

   p = (20.00/100) ;   --------> sequiser  retornar um valor decimal tem que colocar ponto na divisão 

   Bonus_comissao =((servico_indicado + seu_salario)* p) ;

   salario_final = (seu_salario + Bonus_comissao) ;
end

/*CLONAR  TABELAS*/
    CREATE PROCEDURE PRC_CLONAR_TBLEPG
      (INTERVALO1 integer , INTERVALO2 INTEGER)
    AS
    BEGIN
      INSERT INTO CLONAR_TBLEPG
      SELECT * FROM TBLEPG           <- USA O SELECT COMO VALUES
      WHERE codpesepg BETWEEN :INTERVALO1 AND :INTERVALO2;
    END


**********fIM**********
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------


	MySQL


**** Criando um Banco de Dados ****
DDL

create database if not exists Curso_em_Videos
Default collate utf8_general_ci;
Default character set utf8

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** Criando uma Tabela ****
DDL

create table if not exists cursos(
nome varchar (20),
carga int unsigned,
ano dataimes,
descricao text
)charset = 'utf8';


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** Alterando colunas da tabela ****
DDL 

alter table cursos
add column profissao varchar(20) after nome;   --------> adicionando mais uma coluna na tabela

alter table cursos
add remane to programas;   --------> alterando o nome da TABELA 

alter table cursos
add primay key(idcursos);  --------> caso esqueça de colocar chave primária

alter table cursos
modify column profissao varchar(500) not null;      --------> modificando o tipo primitivo e os constraints

alter table cursos
change column profissao trabalho varchar(25) first; --------> trancando o nome e alterando tudo , Obs tem que colocar o nome antigo primeiro 

alter table cursos   --------> apagando uma coluna
drop column profissao;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** Iserindo dados natabela ****
DML

insert into cursos values
('Html',' 40', '2012', 'Para se tornar um dev web'), --------> registros
('Css3',' 50', '2013', 'Para se tornar um dev web');


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**** Modificando registro ****
DML

update cursos
set nome='Html' , ano = '2020'  --------> esse altera um registro  com base no where 
where ano = '2012'
limit 1;


delete from cursos    --------> esse apaga a linha completa  em  que o ano é 2013   com no where
where ano = '2013'
limit 1 ; --> indica a quantidade


truncate cursos ;  -------->  esse apaga todos os registro da tabela

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**************select**************

DQL

describe cursos  ou  desc cursos  --------> mostra todos os componentes/colunas da tabela 

select * from cursos;  --------> mostra todos os registros da sua tabela

select nome , ano form cursos
where ano = '2020'      -------->  filtrar por linha
order by nome desc ;    -------->  mostra o nome , ano , quando os registros forem do ano 2020  e vai ser ordernado  por nome descrecente.


select ano , nome from cursos ------->  filtra por coluna
order by ano, nome;

podemos usar operadores relacionais no whare também : = , < , > , !=  <> , <=, >= 

select nome , profissao from cursos
where  nascimento >=  '2022' 
order by nome;


outros operadores :


* between  significa filtra  um número x até y

select  ano , nome from cursos
where ano between '2000' and '2025' ;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
* in  significa filtra número  x e y e g 

select ano , nome from cursos
where ano in ('2000' , '2015' , '2021')
order by ano , nome;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

*Eu posso combinar os dois 

selec * from cursos
where carga < 30 and totaulas > 20 ;    --------> aperadores lógicos:  and = e , or = ou , not = não 


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
* Filtra registros com as letras parecida ou palavras que começa com determinada letra :  like 

select  *  from cursos
where nome like 'P%' ;


ou eu posso fazer o inverso , filtrar regitros com letrar terminadas com x letras 

select nome from cursos
where nome like '%A' ;  

ou eu posso fazer os dois juntos , obs: essa porcentagem significa carta coringa e ela pode ter qualquer valor ou nenhum : 

select nome from cursos
where nome like '%a%' ;     --------> pode aparecer Amanda , porque o curinga pode ter qualquer letra e essa condição se encaixa nesse requisito.

% = _   essas são as duas cartas curingas , a diferença é que o _ obriga a ter pelo o menos um  character o % pode ser uma character ou nada , numeros atende os dois também.


o outros comando do select:

select max(altura) from pessoas;  --------> vai  selecionar a maior altura 

selec min(altura) from pessoas;   --------> vai  selecionar a menor  altura 

select count(nomes) from pessoas; --------> vai contar quantos nomes que tem na tabela

select sum(anos) from cursos;     --------> vai somar os anos da tabela cursos ;

select distinct nacionalidade from pessoas 
order by nacionalidade;    --------> vai filtra as nacionalidades e não vai mostrar as nacionalidades repetidas. Com o 'order by nacionalidade' vai colocar de ordem alfabética.

select nacionalidade, count(*) from pessoas
group by nacionalidade  ;  --> vai fazer um agrupamento de nacionalidade sendo que são iguais ou difetentes e também com o comando count() podemos saber quantas nacionalidade tem cada grupo ,detro do count() pode ter qualquer coluna.

select avg(salario) from funcionarios 
where sexo = 'F' ;   --> esse avg significa a média , no caso do where  ele é uma condição para que a média seja calculadas dos sálarios das mulheres;

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**************Exercícios select**************

1) Faça uma lista com o nome de todas as mulheres.

R- select nome from pessoas
   where sexo = 'F';

2) Faça uma lista com os dados de todos aqueles que nasceram entre  01/Jan/2000 e 31/Dez/2015.

R- select * from pessoas
   where ano between '2000' and '2015' ;

3) Faça uma lista com o nome de todos os homens que trabalham como Programadores.

R- select nome from pessoas 
   where sexo = 'M' and profissao = 'Programadores';

4) Faça uma lista com os dados de todas as mulheres que nasceram no Brasil e que têm seu nome iniciando com a letra J.

R- select * from pessoas
   where sexo = 'F' and nacionalidade = 'Brasil' and nome like 'J%';

5) Faça uma lista com o nome e nacionalidade de todos os homens que têm Silva no nome, não nasceram no Brasil e pesam menos de 100 KG.

R - select nome , nacionalidade from pessoas
    where sexo = 'M' and nome like '&_Silva&' and not nacionalidade 'Brasil' and peso > 100;

6) Faça uma lista que mostra qual é a maior altura entre os homens que moram no Brasil.

R- select max(altura) from pessoas
   where sexo = 'M' and nacionalidade 'Brasil';

7) Faça uma lista que mostra qual é o menor peso entre as meninas que nasceram fora do Brasil e entre 01/01/1990 e 31/12/2000.

R - select min(peso) from pessoas
    where sexo = 'F' and nacionalidade != 'Brasil' and nascimento between '1990' and '2000';

8) Faça uma lista que mostra quantas mulheres têm mais de 1.90m.

R- select count(altura) from pessoas
   where sexo = 'F' and altura > '1.90'

*****Exercícios de select usando agrupamentos*******

1) Faça uma lista com as profissões dos meninos e seus respectivos quantitativos.

R- select profissao , count(*) from pessoas
   where sexo = 'M'
   group by profissao;

2) Faça uma lista que mostre quantos homens e mulheres nasceram após 01/01/2005

R - select count(*) from pessoas
    group by sexo
    having (select count(*) from pessoas where nascimento >=  '2005'  );


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
**************Fazer backup**************

no menu server >>> Data Export para exportar >> seleciona o banco de dados  e clique no start Export , após isso vai ser gerado um Dumping ou Dump.
Dump é o  passo a  passo  para criar o banco de dados que vc tem no seu servidor , para importar é os mesmo passos , mas é para selecionar o Data Import ... seleciona a pasta onde está o seu Dump.

****fim****
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
-- comandos do Git



Conectando ao repositório remoto

git init

git add README.md

git commit -m "first commit"

git branch -M main

git remote add origin https://Local_do_Seu_repositório_no_GitHub.git

git push -u origin main

OBS : 

qaundo você for criar uma nova branch , cria com outro nome , não repete o mesmo nome da sua branch que vc apagou no local.
 
depois disso você tem que dar o seu primeiro commit (adiciona qualquer arquivo e  usa o 'git gui para add as modificacoes' e depois você vai adicionar o 'commit').

quando você criar uma nova branch, ela não vai ter um  repositório remoto,para resolver isso só basta dar um git push (não pode dar o comando git pull, pois não vai ter uma conexão com o remoto , pois não existe repositório remoto dessa branch). 

se aparecer uma mensagem de fatal  usa este comando que vai da certo : git push --set upstream origin nome_da_sua_branch_que_vc_acabou_de_criar.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
* Outros Comandos

git pull --------> comparar as modificações do seu último repositório

git config --glogal user.name "lucas"

git config --global user user.email "email"

git config --global merge.tool tortoisemerge

git config --global mergetool.tortoisemerge.cmd ""  --------> local onde vc instalou o tortoise

git clone  http://link.git  ou se não der certo foi por causa da permissao, você terá que colocar o seu usuário do gitea e o @ antes do seu usuário exemplo : http://@usuário_do_gitealink.git

git checkout working

git branch treinamento  --------> cirando uma branch

git stash  --------> reseta/suspende  as modificações do começo  e pega todas as modificações  que eu fiz e salva (recorta) até o último commit.

git stash apply  --------> ele aplica as modificações que o git stash suspendeu que eu fiz

git reset --hard --------> vai apagar tudo no seu repositório local até o seu último pull

git reset vai apagar o seu commit e vai voltar (nao usar)

gitk    semelhante ao git log 

na branch de talentos --------> git merge lucas_victor   para unir as branch.

git branch -d <branch>  Exclua um branch no repositório local , não apaga no remoto,para apagar no repositório remoto é muito perigoso , pois tem que informar o caminho, melhor não usar esse comando

git config --list  para listar as configurações do seu git
 
****fim****
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
TortoiseGit

/*Resolvendo Conflitos*/

case de um conflito , vc terá que resolver com o tortoise e depois disso vc vai fazer um commit,  de preferença com o git gui , depois vc vai colocar o comando de git pull para atualizar (caso de mais conflitos  vc resolve de novo ) e depois disso vc vai usar o comando de git push

****fim****

