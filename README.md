                                 Trabalho de Banco de Dados 





TURMA :204

Nome dos integrantes:  Isaac Matos de Souza   

Rebeca Duarte Arcanjo

José Tadeu Silva Viana da Conceição

Eder Henrique J da silva

Miguel Arcanjo Delogo



-------------------------------------------------------------------

De inicio do trabalho a ideia é bem simples: montar um banco de dados que ajuda a organizar informações de alimentos, ingredientes, calorias e umas paradas que têm a ver com saúde e bem-estar tipo saber o que você tá comendo

- ideia principal:

O foco é montar uma base de dados onde eu consiga guardar informacoes de produtos alimentares. Tipo nome, calorias, código de barras, se tem açúcar demais, e por aí vai.
Serve pra ajudar quem quer se alimentar melhor ou entender melhor o que tá consumindo.

- MYSQL                                              para criar o banco precisamos utilizar a primeira linha de codigo q é:
CREATE DATABASE nome do banco q é (nutriscan); e para usarmos a database que criamos ou ja esta criada, utilizamos o USE e o nome do banco q é (nutriscan); 
Aí com isso eu já estava dentro do banco e comecei a montar as tabelas.

- Tabela dos produtos

Criei a tabela produtos, onde eu guardo:

nome do produto,

código,

calorias,

fabricante,

código de barras,

se tem alto teor de açúcar ou não (trabalhando com as respostas (sim ou não)),

e a data que foi cadastrado.

- O codigo que usamos foi esse:                        

CREATE TABLE produtos (
 id INT AUTO_INCREMENT PRIMARY KEY,
 codigo VARCHAR(100),
 nome VARCHAR(255),
 calorias VARCHAR(50),
 fabricante VARCHAR(100),
 codigo_barras VARCHAR(100) UNIQUE,
 alto_teor_acucar BOOLEAN DEFAULT FALSE, 
 observacoes TEXT,
 data_cadastro DATETIME DEFAULT CURRENT_TIMESTAMP
 ); 

oque rola aqui:

Esse código cria a tabela produtos, onde ficam as infos principais dos alimentos. O id identifica cada produto e vai aumentando sozinho. O codigo e o nome são pra identificar o produto. calorias e fabricante falam quantas calorias tem e quem fez. codigo_barras não pode repetir, porque é único pra cada produto. alto_teor_acucar marca se o produto tem muito ou pouco açúcar (e ele vem falso por padrão). o observacoes serve pra anotar qualquer coisa extra. E o data_cadastro já pega a data e hora que foi cadastrado, sozinho. Tudo organizado pra depois ligar com os ingredientes.

- Tabela dos ingredientes:

Pra não ficar aquela bagunça de colocar os ingredientes tudo junto na mesma tabela, eu criei uma tabela separada chamada ingredientes.

Ela é ligada com a de produtos pelo produto_id, e é assim:

CREATE TABLE ingredientes ( 
   id INT AUTO_INCREMENT PRIMARY KEY,
   produto_id INT NOT NULL, 
   nome_ingrediente VARCHAR(255) NOT NULL,
   FOREIGN KEY (produto_id) REFERENCES produtos(id)
ON DELETE CASCADE
 ); 

oque rola aqui:

Essa tabela é pros ingredientes dos produtos. O id identifica cada ingrediente. O produto_id liga esse ingrediente a um produto da outra tabela. O nome_ingrediente é só o nome mesmo, tipo "Açúcar".

O FOREIGN KEY faz a conexão com a tabela produtos, E o ON DELETE CASCADE é tipo: se eu apagar um produto, os ingredientes ligados a ele já somem junto, tipo um efeito dominó.

Coca-Cola:

Pra testar isso, eu cadastrei a Coca-Cola como exemplo assim:

INSERT INTO produtos (codigo, nome, calorias) 
VALUES ('C001', 'Coca-Cola', '140'); 

e outros exemplos tambem como:

INSERT INTO produtos (nome, calorias, fabricante, ingredientes) 
VALUES ('Granola Natural',120,'Granola Vida', 'Aveia, mel, castanhas');

E pronto ficou com os ingredientes organizados

Se for olhar no diagrama MySQL Workbench, tu vai ver a tabela produtos ligada com a ingredientes por uma setinha, bem simples e facil.

E para depois a gente esta pensando em fazer umas outras consultas boas, tipo:
“me mostra os produtos com mais calorias”, ou “me mostra os que têm açúcar” e etc.
