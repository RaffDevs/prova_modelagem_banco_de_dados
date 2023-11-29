# Prova Modelagem Banco de Dados


### Descrição

<p>
  No sistema de controle de alunos desenvolvido pela "EducaSimples", as entidades e seus relacionamentos proporcionam uma visão organizada das informações acadêmicas na escola primária.

Cada aluno, como Maria da Silva, é identificado por um ID único, e seu cadastro inclui informações como nome, data de nascimento e endereço. Esses alunos são associados a responsáveis, como João da Silva, através de um relacionamento específico (N:1), permitindo que cada responsável esteja vinculado a vários alunos, mas cada aluno tenha apenas um responsável.

Além disso, os alunos são agrupados em turmas, como o 4º Ano da Prof. Ana Souza, proporcionando um método eficiente de gerenciar grupos de estudantes. Cada aluno pertence a uma única turma (N:1), enquanto uma turma pode conter vários alunos.

Para avaliar o desempenho acadêmico, o sistema registra notas associadas a cada aluno. Maria da Silva, por exemplo, pode ter várias notas atribuídas a ela. Esse relacionamento (1:N) permite uma visão detalhada do progresso individual de cada aluno.

Adicionalmente, as disciplinas, como Matemática, são registradas no sistema e associadas às turmas. Este relacionamento muitos-para-muitos (M:N) possibilita que uma disciplina seja ensinada em várias turmas, enquanto uma turma pode abranger várias disciplinas.

</p>


# Modelagem Conceitual

![DER-modelagem](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/bcdbe949-7f7e-42b5-bdc1-1618d7865857)



# Modelagem Lógica

![modelo-logico](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/2c0d5ca5-078b-46b3-9e72-294ffb0a49df)


# Modelagem Fisica
 - Banco de dados: SQL Server
### Criação das tabelas
````
-- Tabela Endereco
CREATE TABLE Endereco (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    rua VARCHAR(100) NOT NULL,
    bairro VARCHAR(100) NOT NULL,
    numero VARCHAR(100) NOT NULL,
    cep CHAR(8) NOT NULL
);

-- Tabela Disciplina
CREATE TABLE Disciplina (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    nome VARCHAR(100) NOT NULL
);

-- Tabela Responsavel
CREATE TABLE Responsavel (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    nome_completo VARCHAR(100),
    data_de_nascimento DATE,
    endereco_id INT,
    FOREIGN KEY (endereco_id) REFERENCES Endereco(id)
);

-- Tabela Turma
CREATE TABLE Turma (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    periodo INT NOT NULL,
    curso VARCHAR(100) NOT NULL,
    disciplina_id INT NOT NULL,
    FOREIGN KEY (disciplina_id) REFERENCES Disciplina(id)
);

-- Tabela Aluno
CREATE TABLE Aluno (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    nome_completo VARCHAR(100),
    data_de_nascimento DATE,
    endereco_id INT,
    responsavel_id INT,
    turma_id INT,
    FOREIGN KEY (endereco_id) REFERENCES Endereco(id),
    FOREIGN KEY (responsavel_id) REFERENCES Responsavel(id),
    FOREIGN KEY (turma_id) REFERENCES Turma(id)
);

-- Tabela Telefone
CREATE TABLE Telefone (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    numero VARCHAR(12) NOT NULL,
    responsavel_id INT NOT NULL,
    FOREIGN KEY (responsavel_id) REFERENCES Responsavel(id)
);

-- Tabela Nota
CREATE TABLE Nota (
    id INT PRIMARY KEY IDENTITY(1,1) NOT NULL,
    valor INT NOT NULL,
    disciplina_id INT NOT NULL,
    aluno_id INT NOT NULL,
    FOREIGN KEY (disciplina_id) REFERENCES Disciplina(id),
    FOREIGN KEY (aluno_id) REFERENCES Aluno(id)
);
````

![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/a29332ca-b662-49d1-973a-49a47206f79c)


# Inserção de dados

````
-- Tabela Endereco
INSERT INTO Endereco (rua, bairro, numero, cep)
VALUES
('Rua das Flores', 'Jardim Primavera', '100', '12345-678'),
('Rua dos Pássaros', 'Vila Nova', '200', '87654-321'),
('Rua dos Ipês', 'Parque dos Ipês', '300', '56789-012'),
('Rua das Rosas', 'Jardim das Rosas', '400', '45678-901'),
('Rua dos Cravos', 'Vila dos Cravos', '500', '34567-890'),
('Rua das Margaridas', 'Parque das Margaridas', '600', '23456-789'),
('Rua dos Lírios', 'Jardim dos Lírios', '700', '12345-678'),
('Rua das Orquídeas', 'Vila das Orquídeas', '800', '87654-321'),
('Rua dos Girassóis', 'Parque dos Girassóis', '900', '56789-012'),
('Rua das Hortênsias', 'Jardim das Hortênsias', '1000', '45678-901'),
('Rua dos Gladiolos', 'Vila dos Gladiolos', '1100', '34567-890'),
('Rua dos Antúrios', 'Parque dos Antúrios', '1200', '23456-789'),
('Rua das Begônias', 'Jardim das Begônias', '1300', '12345-678'),
('Rua dos Azaleias', 'Vila das Azaleias', '1400', '87654-321'),
('Rua das Bromélias', 'Parque das Bromélias', '1500', '56789-012'),
('Rua das Coqueiros', 'Jardim dos Coqueiros', '1600', '45678-901'),
('Rua das Palmeiras', 'Vila das Palmeiras', '1700', '34567-890'),
('Rua das Jabuticabeiras', 'Parque das Jabuticabeiras', '1800', '23456-789'),
('Rua das Pitangueiras', 'Jardim das Pitangueiras', '1900', '12345-678'),
('Rua das Mangueiras', 'Vila das Mangueiras', '2000', '87654-321');

-- Tabela Disciplina
INSERT INTO Disciplina (nome)
VALUES
('Matemática', 'Português', 'Inglês', 'Espanhol', 'Ciências', 'História', 'Geografia', 'Biologia', 'Física', 'Química'),
('Filosofia', 'Sociologia', 'Artes', 'Educação Física', 'Informática', 'Ética', 'Religião', 'Psicologia', 'Pedagogia', 'Letras');

-- Tabela Responsavel
INSERT INTO Responsavel (nome_completo, data_de_nascimento, endereco_id)
VALUES
('João Silva', '1980-01-01', 1),
('Maria Souza', '1985-02-02', 2),
('José Santos', '1990-03-03', 3),
('Ana Oliveira', '1995-04-04', 4),
('Pedro Ferreira', '2000-05-05', 5),
('Luisa Alves', '2005-06-06', 6),
('Antônio Campos', '2010-07-07', 7),
('Mariana Pereira', '2015-08-08', 8),
('Paulo Costa', '2020-09-09', 9),
('Rafaela Mendes', '2023-10-10', 10),
('Bruno Martins', '1980-01-01', 11),
('Carla Nascimento', '1985-02-01', 11)


-- Tabela Turma
INSERT INTO Turma (periodo, curso, disciplina_id)
VALUES
(1, 'Ensino Fundamental', 1),
(1, 'Ensino Fundamental', 2),
(1, 'Ensino Fundamental', 3),
(1, 'Ensino Fundamental', 4),
(1, 'Ensino Fundamental', 5),
(1, 'Ensino Fundamental', 6),
(1, 'Ensino Fundamental', 7),
(1, 'Ensino Fundamental', 8),
(1, 'Ensino Fundamental', 9),
(1, 'Ensino Fundamental', 10),
(2, 'Ensino Médio', 11),
(2, 'Ensino Médio', 12),
(2, 'Ensino Médio', 13),
(2, 'Ensino Médio', 14),
(2, 'Ensino Médio', 15),
(2, 'Ensino Médio', 16),
(2, 'Ensino Médio', 17),
(2, 'Ensino Médio', 18),
(2, 'Ensino Médio', 19),
(2, 'Ensino Médio', 20);

-- Tabela Aluno
INSERT INTO Aluno (nome_completo, data_de_nascimento, endereco_id, responsavel_id, turma_id)
VALUES
('João da Silva', '2010-01-01', 1, 1, 1),
('Maria da Souza', '2011-02-02', 2, 2, 2),
('José do Santos', '2012-03-03', 3, 3, 3),
('Ana da Oliveira', '2013-04-04', 4, 4, 4),
('Pedro do Ferreira', '2014-05-05', 5, 5, 5),
('Luisa da Alves', '2015-06-06', 6, 6, 6),
('Antônio do Campos', '2016-07-07', 7, 7, 7),
('Mariana da Pereira', '2017-08-08', 8, 8, 8),
('Paulo do Costa', '2018-09-09', 9, 9, 9),
('Rafaela da Mendes', '2019-10-10', 10, 10, 10),
('Bruno do Martins', '2020-11-11', 11, 11, 11),
('Carla do Nascimento', '2021-12-12', 12, 12, 12),
('Daniel da Lima', '2022-01-13', 13, 13, 13),
('Eduarda da Silva', '2023-02-14', 14, 14, 14),
('Felipe do Souza', '2024-03-15', 15, 15, 15),
('Gabriela do Santos', '2025-04-16', 16, 16, 16),
('Henrique da Oliveira', '2026-05-17', 17, 17, 17),
('Isabela do Ferreira', '2027-06-18', 18, 18, 18),
('João da Alves', '2028-07-19', 19, 19, 19),
('Maria do Campos', '2029-08-20', 20, 20, 20);


-- Tabela Telefone
INSERT INTO Telefone (numero, responsavel_id)
VALUES
('(11) 9999-9999', 1),
('(12) 8888-8888', 2),
('(13) 7777-7777', 3),
('(14) 6666-6666', 4),
('(15) 5555-5555', 5),
('(16) 4444-4444', 6),
('(17) 3333-3333', 7),
('(18) 2222-2222', 8),
('(19) 1111-1111', 9),
('(20) 0000-0000', 10),
('(21) 9999-9999', 11),
('(22) 8888-8888', 12),
('(23) 7777-7777', 13),
('(24) 6666-6666', 14),
('(25) 5555-5555', 15),
('(26) 4444-4444', 16),
('(27) 3333-3333', 17),
('(28) 2222-2222', 18),
('(29) 1111-1111', 19),
('(30) 0000-0000', 20);



-- Tabela Nota
INSERT INTO Nota (valor, disciplina_id, aluno_id)
VALUES
(10, 1, 1),
(9, 2, 2),
(8, 3, 3),
(7, 4, 4),
(6, 5, 5),
(5, 6, 6),
(4, 7, 7),
(3, 8, 8),
(2, 9, 9),
(1, 10, 10),
(10, 11, 11),
(9, 12, 12),
(8, 13, 13),
(7, 14, 14),
(6, 15, 15),
(5, 16, 16),
(4, 17, 17),
(3, 18, 18),
(2, 19, 19),
(1, 20, 20);

````

### Insert Aluno
![INSERT_ALUNO](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/16283a64-dd22-4c0e-a105-544dbf87c6df)

### Insert Disciplina
![INSERT_DISCIPLINA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/d05acf2d-6bfd-4959-8564-420c80f25f07)

### Insert Endereço
![INSERT_ENDERECO](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/296746db-cf78-4d2b-8b1f-a0f669dee9c8)

### Insert Responsavel
![INSERT_RESPONSAVEL](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/0dff8f0f-1f2b-428b-bbe8-173fd77cc3c1)

### Insert Nota
![INSERT_NOTA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/a5c7d9e7-261f-491f-a047-ab4ca26505cf)

### Insert Telefone
![INSERT_TELEFONE](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/c569ec9e-0c0c-42a6-ba00-e620c6387f09)

### Insert Turma
![INSERT_TURMA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/95a5f50a-5e9e-41e9-bac4-eae72e561596)


# CRUD

````
# ------ ENDERECO --------- #

-- Create (INSERT)
INSERT INTO Endereco (rua, bairro, numero, cep)
VALUES ('Rua A', 'Bairro 1', '123', '12345-678');

-- Update (UPDATE)
UPDATE Endereco
SET rua = 'Fatequei Legalzim'
WHERE id = 23;

-- Delete (DELETE)
DELETE FROM Endereco
WHERE id = 24;

-- Read (SELECT)
SELECT * FROM Endereco;

# ------ DISCIPLINA --------- #

-- Create (INSERT)
INSERT INTO Disciplina (nome)
VALUES ('Programação em Assembly');

-- Update (UPDATE)
UPDATE Disciplina
SET nome = 'Curso de VIM'
WHERE id = 20;

-- Delete (DELETE)
DELETE FROM Disciplina
WHERE id = 1;

-- Read (SELECT)
SELECT * FROM Disciplina;


# ------ RESPONSAVEL --------- #

-- Create (INSERT)
INSERT INTO Responsavel (nome_completo, data_de_nascimento, endereco_id)
VALUES ('João Silva', '1980-01-01', 4);

-- Read (SELECT)
SELECT * FROM Responsavel;

-- Update (UPDATE)
UPDATE Responsavel
SET nome_completo = 'joãozim ZN'
WHERE id = 19;

-- Delete (DELETE)
DELETE FROM Responsavel
WHERE id = 25;


# ------ ALUNO --------- #

-- Create (INSERT)
INSERT INTO Aluno (nome_completo, data_de_nascimento, endereco_id, responsavel_id, turma_id)
VALUES ('Maria da Silva', '2000-01-01', 1, 1, 1);

-- Update (UPDATE)
UPDATE Aluno
SET nome_completo = 'Novo Nome'
WHERE id = 1;

-- Delete (DELETE)
DELETE FROM Aluno
WHERE id = 1;

-- Read (SELECT)
SELECT * FROM Aluno;


# ------ TELEFONE --------- #

-- Create (INSERT)
INSERT INTO Telefone (numero, responsavel_id)
VALUES ('123456789', 1);

-- Update (UPDATE)
UPDATE Telefone
SET numero = '987654321'
WHERE id = 1;

-- Delete (DELETE)
DELETE FROM Telefone
WHERE id = 1;

-- Read (SELECT)
SELECT * FROM Telefone;

# ------ TURMA --------- #

-- Create (INSERT)
INSERT INTO Turma (periodo, curso, disciplina_id)
VALUES (1, 'Engenharia', 1);

-- Read (SELECT)
SELECT * FROM Turma;

-- Update (UPDATE)
UPDATE Turma
SET curso = 'Novo Curso'
WHERE id = 1;

-- Delete (DELETE)
DELETE FROM Turma
WHERE id = 1;

# ------ NOTA --------- #

-- Create (INSERT)
INSERT INTO Nota (valor, disciplina_id, aluno_id)
VALUES (90, 1, 1);

-- Read (SELECT)
SELECT * FROM Nota;

-- Update (UPDATE)
UPDATE Nota
SET valor = 95
WHERE id = 1;

-- Delete (DELETE)
DELETE FROM Nota
WHERE id = 1;


````

### Endereço
![CRUD_ENDERECO](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/e7d144fb-3ebd-4adc-b394-11b43fd0fed3)

### DISCIPLINA
![CRUD_DISCIPLINA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/d0274d35-1132-45f9-b5f8-fbc8f3734640)

### ALUNO
![CRUD_ALUNO](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/3b66e2ec-e627-44b4-a373-db9e40ada1ae)

### NOTA
![CRUD_NOTA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/f515e8a5-c88c-4018-83dd-20f89ef7f24b)

### RESPONSAVEL
![CRUD_RESPONSAVEL](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/6dd0e1e0-a830-4789-b69f-8e58d34e180d)

### TELEFONE
![CRUD_TELEFONE](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/1d9c77e2-aaf4-4106-87d6-8c33cf68649c)

### TURMA 
![CRUD_TURMA](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/508e6216-57ab-4ff5-9e88-474b9fbce1d3)



# Relatorios

````
SELECT Aluno.nome_completo AS NomeAluno, Responsavel.nome_completo AS NomeResponsavel
FROM Aluno
JOIN Responsavel ON Aluno.responsavel_id = Responsavel.id;
````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/e163f67e-a380-422f-95d1-abbb6ba189b9)



````
SELECT Disciplina.nome AS NomeDisciplina, Turma.curso AS CursoTurma
FROM Disciplina
JOIN Turma ON Disciplina.turma_id = Turma.id;
````

![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/aa3c094a-b063-448a-ac30-13430d8d1232)



````
SELECT Aluno.nome_completo AS NomeAluno, Nota.valor AS Nota
FROM Aluno
JOIN Nota ON Aluno.id = Nota.aluno_id
WHERE Nota.disciplina_id = 1;
````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/7d37916c-b46a-43c0-a127-f243d8c1d2f3)


````
SELECT Responsavel.nome_completo AS NomeResponsavel, Telefone.numero AS NumeroTelefone
FROM Responsavel
JOIN Telefone ON Responsavel.id = Telefone.responsavel_id;

````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/65c2dbbe-4d2e-462c-84d6-3ad6b5320178)


````
SELECT Aluno.nome_completo AS NomeAluno, Turma.curso AS CursoTurma
FROM Aluno
JOIN Turma ON Aluno.turma_id = Turma.id
WHERE Turma.id = 1; -- Substitua 1 pelo ID da turma desejada.


````

![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/c5bd8190-2cb2-4bd7-8d80-e395302867f2)



`````
SELECT nome_completo AS NomeAluno, data_de_nascimento
FROM Aluno
ORDER BY data_de_nascimento;

`````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/30fd9e93-c3fb-41ab-ac07-b74257cdc45c)


````
SELECT DISTINCT Responsavel.nome_completo AS NomeResponsavel
FROM Responsavel
JOIN Aluno ON Responsavel.id = Aluno.responsavel_id
JOIN Nota ON Aluno.id = Nota.aluno_id
WHERE Nota.valor > 90;

````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/eeae41ce-136b-4dae-b27c-94ef6f88c9f5)


````

SELECT Disciplina.nome AS NomeDisciplina, COUNT(DISTINCT Turma.id) AS NumTurmas
FROM Disciplina
JOIN Turma ON Disciplina.turma_id = Turma.id
GROUP BY Disciplina.nome
HAVING COUNT(DISTINCT Turma.id) > 1;

````

![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/df005669-af2b-44d8-a8ae-e34ba929284e)


````
SELECT Aluno.nome_completo AS NomeAluno, Telefone.numero AS NumeroTelefone
FROM Aluno
JOIN Telefone ON Aluno.responsavel_id = Telefone.responsavel_id;
````
![image](https://github.com/RaffDevs/prova_modelagem_banco_de_dados/assets/56967435/04f45157-ca25-47ee-b6c0-e0d4e26dd474)

