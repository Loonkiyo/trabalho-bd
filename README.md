IF OBJECT_ID('Falta', 'U') IS NOT NULL DROP TABLE Falta;
IF OBJECT_ID('Nota', 'U') IS NOT NULL DROP TABLE Nota;
IF OBJECT_ID('Aluno', 'U') IS NOT NULL DROP TABLE Aluno;
IF OBJECT_ID('Disciplina', 'U') IS NOT NULL DROP TABLE Disciplina;
IF OBJECT_ID('Professor', 'U') IS NOT NULL DROP TABLE Professor;
IF OBJECT_ID('Curso', 'U') IS NOT NULL DROP TABLE Curso;
GO
 
CREATE TABLE Curso (
    codigo_curso INT PRIMARY KEY IDENTITY(1,1),
    nome_curso VARCHAR(100) NOT NULL,
    area_curso VARCHAR(50) NOT NULL
);
 
CREATE TABLE Professor (
    codigo_professor INT PRIMARY KEY IDENTITY(1,1),
    nome_professor VARCHAR(100) NOT NULL,
    especialidade VARCHAR(50)
);
 
CREATE TABLE Disciplina (
    codigo_disciplina INT PRIMARY KEY IDENTITY(1,1),
    nome_disciplina VARCHAR(100) NOT NULL,
    codigo_curso INT NOT NULL,
    codigo_professor INT NOT NULL,
    carga_horaria INT,
    FOREIGN KEY (codigo_curso) REFERENCES Curso(codigo_curso),
    FOREIGN KEY (codigo_professor) REFERENCES Professor(codigo_professor)
);
 
CREATE TABLE Aluno (
    codigo_aluno INT PRIMARY KEY IDENTITY(1,1),
    nome_aluno VARCHAR(100) NOT NULL,
    endereco_aluno VARCHAR(200),
    cidade_aluno VARCHAR(50),
    telefone_aluno VARCHAR(20),
    codigo_curso INT NOT NULL,
    FOREIGN KEY (codigo_curso) REFERENCES Curso(codigo_curso)
);
 
CREATE TABLE Nota (
    codigo_nota INT PRIMARY KEY IDENTITY(1,1),
    codigo_aluno INT NOT NULL,
    codigo_disciplina INT NOT NULL,
    nota VARCHAR(2) NOT NULL,
    data_avaliacao DATE,
    FOREIGN KEY (codigo_aluno) REFERENCES Aluno(codigo_aluno),
    FOREIGN KEY (codigo_disciplina) REFERENCES Disciplina(codigo_disciplina)
);
 
CREATE TABLE Falta (
    codigo_falta INT PRIMARY KEY IDENTITY(1,1),
    codigo_aluno INT NOT NULL,
    codigo_disciplina INT NOT NULL,
    data_falta DATE NOT NULL,
    quantidade_faltas INT DEFAULT 1,
    FOREIGN KEY (codigo_aluno) REFERENCES Aluno(codigo_aluno),
    FOREIGN KEY (codigo_disciplina) REFERENCES Disciplina(codigo_disciplina)
);
GO
 
INSERT INTO Curso (nome_curso, area_curso) VALUES
('Administração', 'Gestão'),
('Informática', 'Tecnologia'),
('Contabilidade', 'Gestão'),
('Desenvolvimento de Sistemas', 'Tecnologia');
GO
 
INSERT INTO Professor (nome_professor, especialidade) VALUES
('Andrea', 'Gestão Empresarial'),
('Carlos', 'Programação'),
('Mariana', 'Banco de Dados'),
('Roberto', 'Finanças'),
('Patricia', 'Marketing');
GO
 
INSERT INTO Disciplina (nome_disciplina, codigo_curso, codigo_professor, carga_horaria) VALUES
('Gestão de Pessoas', 1, 1, 80),
('Matemática Financeira', 1, 4, 60),
('Marketing Digital', 1, 5, 40),
('Programação em Java', 2, 2, 100),
('Banco de Dados', 2, 3, 80),
('Redes de Computadores', 2, 2, 60),
('Algoritmos', 2, 2, 80),
('Contabilidade Geral', 3, 4, 70);
GO
 
INSERT INTO Aluno (nome_aluno, endereco_aluno, cidade_aluno, telefone_aluno, codigo_curso) VALUES
('João Silva', 'Rua A, 123', 'Sorocaba', '(15) 9999-1111', 1),
('Maria Santos', 'Av B, 456', 'Sorocaba', '(15) 9999-2222', 2),
('Pedro Oliveira', 'Rua C, 789', 'Itu', '(15) 9999-3333', 1),
('Ana Costa', 'Rua D, 321', 'Sorocaba', '(15) 9999-4444', 2),
('Carlos Lima', 'Av E, 654', 'Votorantim', '(15) 9999-5555', 3),
('Juliana Pereira', 'Rua F, 987', 'Sorocaba', '(15) 9999-6666', 2),
('Fernando Souza', 'Rua G, 147', 'Sorocaba', '(15) 9999-7777', 1),
('Amanda Rocha', 'Av H, 258', 'Itu', '(15) 9999-8888', 2),
('Ricardo Alves', 'Rua I, 369', 'Sorocaba', '(15) 9999-9999', 3),
('Patricia Mendes', 'Av J, 741', 'Sorocaba', '(15) 9999-0000', 1),
('André Oliveira', 'Rua K, 852', 'Sorocaba', '(15) 9999-1212', 2),
('Alice Santos', 'Av L, 963', 'Itu', '(15) 9999-2323', 1);
GO
 
INSERT INTO Nota (codigo_aluno, codigo_disciplina, nota, data_avaliacao) VALUES
(1, 1, 'MB', '15/01/2024'),
(1, 2, 'B', '20/01/2024'),
(2, 4, 'MB', '18/01/2024'),
(2, 5, 'MB', '22/01/2024'),
(3, 1, 'R', '16/01/2024'),
(3, 3, 'B', '25/01/2024'),
(4, 4, 'MB', '19/01/2024'),
(4, 6, 'B', '28/01/2024'),
(5, 8, 'MB', '30/01/2024'),
(6, 4, 'MB', '17/01/2024'),
(6, 5, 'MB', '24/01/2024'),
(7, 1, 'B', '21/01/2024'),
(8, 4, 'MB', '26/01/2024'),
(9, 8, 'R', '29/01/2024'),
(10, 1, 'MB', '27/01/2024'),
(10, 2, 'MB', '01/02/2024'),
(2, 6, 'B', '02/02/2024'),
(4, 7, 'I', '03/02/2024'),
(6, 7, 'MB', '04/02/2024'),
(8, 5, 'I', '05/02/2024');
GO
 
INSERT INTO Falta (codigo_aluno, codigo_disciplina, data_falta, quantidade_faltas) VALUES
(1, 1, '10/01/2024', 2),
(1, 2, '12/01/2024', 1),
(2, 4, '11/01/2024', 1),
(2, 5, '15/01/2024', 3),
(3, 1, '08/01/2024', 1),
(3, 3, '20/01/2024', 2),
(4, 4, '09/01/2024', 1),
(4, 6, '22/01/2024', 1),
(5, 8, '25/01/2024', 2),
(6, 4, '12/01/2024', 1),
(6, 5, '18/01/2024', 1),
(7, 1, '14/01/2024', 3),
(8, 4, '19/01/2024', 1),
(9, 8, '23/01/2024', 2),
(10, 1, '16/01/2024', 1),
(10, 2, '30/01/2024', 1),
(3, 1, '25/01/2024', 1),
(2, 4, '28/01/2024', 2);
GO
 
SELECT * FROM Aluno;
GO
 
SELECT * FROM Curso;
GO
 
SELECT * FROM Aluno WHERE cidade_aluno = 'Sorocaba';
GO
 
SELECT d.* 
FROM Disciplina d
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE c.nome_curso = 'Administração';
GO
 
SELECT d.* 
FROM Disciplina d
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE c.nome_curso = 'Informática';
GO
 
SELECT d.* 
FROM Disciplina d
INNER JOIN Professor p ON d.codigo_professor = p.codigo_professor
WHERE p.nome_professor = 'Andrea';
GO
 
SELECT n.codigo_disciplina, d.nome_disciplina, n.nota, n.data_avaliacao
FROM Nota n
INNER JOIN Disciplina d ON n.codigo_disciplina = d.codigo_disciplina
WHERE n.codigo_aluno = 10;
 
SELECT f.codigo_disciplina, d.nome_disciplina, f.data_falta, f.quantidade_faltas
FROM Falta f
INNER JOIN Disciplina d ON f.codigo_disciplina = d.codigo_disciplina
WHERE f.codigo_aluno = 10;
GO
 
SELECT AVG(f.quantidade_faltas * 1.0) as media_faltas
FROM Falta f
INNER JOIN Disciplina d ON f.codigo_disciplina = d.codigo_disciplina
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE c.nome_curso = 'Informática';
GO
 
SELECT SUM(f.quantidade_faltas) as total_faltas
FROM Falta f
INNER JOIN Disciplina d ON f.codigo_disciplina = d.codigo_disciplina
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE c.nome_curso = 'Administração';
GO
 
SELECT 
    d.codigo_disciplina,
    d.nome_disciplina,
    COUNT(n.nota) as quantidade_MB
FROM Disciplina d
LEFT JOIN Nota n ON d.codigo_disciplina = n.codigo_disciplina AND n.nota = 'MB'
GROUP BY d.codigo_disciplina, d.nome_disciplina
ORDER BY quantidade_MB DESC;
GO
 
SELECT SUM(quantidade_faltas) as total_faltas_aluno_3
FROM Falta 
WHERE codigo_aluno = 3;
GO
 
SELECT 
    c.nome_curso,
    COUNT(n.nota) as quantidade_MB
FROM Nota n
INNER JOIN Disciplina d ON n.codigo_disciplina = d.codigo_disciplina
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE c.nome_curso = 'Informática' AND n.nota = 'MB'
GROUP BY c.nome_curso;
GO
 
SELECT 
    c.nome_curso as turma,
    n.nota,
    COUNT(n.nota) as quantidade
FROM Nota n
INNER JOIN Disciplina d ON n.codigo_disciplina = d.codigo_disciplina
INNER JOIN Curso c ON d.codigo_curso = c.codigo_curso
WHERE n.nota IN ('MB', 'B', 'R', 'I')
GROUP BY c.nome_curso, n.nota
ORDER BY c.nome_curso, n.nota;
GO
 
SELECT a.codigo_aluno, a.nome_aluno, c.nome_curso
FROM Aluno a
INNER JOIN Curso c ON a.codigo_curso = c.codigo_curso
WHERE c.nome_curso IN ('Informática', 'Administração')
ORDER BY c.nome_curso, a.nome_aluno;
GO
 
SELECT *
FROM Disciplina
WHERE nome_disciplina LIKE '%o%' OR nome_disciplina LIKE '%O%';
GO
 
SELECT *
FROM Aluno
WHERE nome_aluno LIKE 'A%';
GO
