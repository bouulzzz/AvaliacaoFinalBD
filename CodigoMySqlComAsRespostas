CREATE DATABASE database_prova;
USE database_prova;

CREATE TABLE curso (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    area VARCHAR(255) NOT NULL
);

CREATE TABLE instituicao (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    sigla VARCHAR(10) NOT NULL
);

CREATE TABLE professor (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    curso_id INT NOT NULL,
    area_atuacao VARCHAR(255) NOT NULL,
    FOREIGN KEY (curso_id) REFERENCES curso(id)
);

CREATE TABLE projeto (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    resumo TEXT NOT NULL,
    responsavel_professor_id INT NOT NULL,
    colaborador_professor_id INT,
    instituicao_id INT NOT NULL,
    FOREIGN KEY (responsavel_professor_id) REFERENCES professor(id),
    FOREIGN KEY (colaborador_professor_id) REFERENCES professor(id),
    FOREIGN KEY (instituicao_id) REFERENCES instituicao(id)
);

INSERT INTO curso (id, nome, area) VALUES
(1, 'Ciência da Computação', 'Tecnologia'),
(2, 'Sistemas de Informação', 'Tecnologia'),
(3, 'Filosofia', 'Sociais');

INSERT INTO instituicao (id, nome, sigla) VALUES
(10, 'Universidad Franciscana', 'UFN'),
(20, 'Universidade Federal de Santa Maria', 'UFSM');

INSERT INTO professor (id, nome, email, curso_id, area_atuacao) VALUES
(1, 'Alexandre Zamberlan', 'alexz@ufn.edu.br', 1, 'Tecnologia'),
(2, 'Ana Paula', 'apc@ufn.edu.b', 1, 'Tecnologia'),
(3, 'Sylvio Garcia', 'sylvio@ufn.edu.br', 2, 'Tecnologia'),
(4, 'Mirkos Martins', 'mirkos@ufn.edu.br', 1, 'Tecnologia');

INSERT INTO projeto (id, titulo, resumo, responsavel_professor_id, colaborador_professor_id, instituicao_id) VALUES
(1, 'Web Crawler', 'Trabalho do Zamba', 1, NULL, 10),
(2, 'SirPerf', 'Sistema de perfusão', 1, 3, 10),
(3, 'OdontoTren', 'Sistema de gestão de atendimento', 2, 3, 20),
(4, 'Avida', 'Sistema de acompanhamento psiquiátrico', 1, NULL, 10);


-- 4 - Descubra quais os projetos da instituição UFN. --

SELECT p.titulo
FROM projeto p
JOIN instituicao i ON p.instituicao_id = i.id
WHERE i.sigla = 'UFN';

-- 5 - Mostre os professores que não possuem projetos submetidos --

SELECT professor.nome
FROM professor
WHERE professor.id NOT IN (
    SELECT projeto.responsavel_professor_id
    FROM projeto
);

-- 6 - Mostre todos os projetos enviados do professor Alexandre Zamberlan --

SELECT p.titulo
FROM projeto p
JOIN professor pr ON p.responsavel_professor_id = pr.id
WHERE pr.nome = 'Alexandre Zamberlan';

-- 7 - Exiba quantos projetos foram submetidos --

SELECT COUNT(*) AS total_projetos
FROM projeto;

-- 8 - Mostre os projetos que não possuem colaboradores --

SELECT titulo
FROM projeto
WHERE colaborador_professor_id IS NULL;

-- 9 - Mostre os projetos que estão vinculados a área de Tecnologia. --

SELECT p.titulo
FROM projeto p
JOIN professor pr ON p.responsavel_professor_id = pr.id
JOIN curso c ON pr.curso_id = c.id
WHERE c.area = 'Tecnologia';

-- 10 - Mostre os projetos vinculados a cada curso. --

SELECT c.nome AS curso, p.titulo AS projeto
FROM projeto p
JOIN professor pr ON p.responsavel_professor_id = pr.id
JOIN curso c ON pr.curso_id = c.id
ORDER BY c.nome, p.titulo;
