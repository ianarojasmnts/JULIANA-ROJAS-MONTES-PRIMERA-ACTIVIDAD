# JULIANA-ROJAS-MONTES-PRIMERA-ACTIVIDAD
Primera actividad
CREATE DATABASE Academiadebaile13;

USE Academiadebaile13;

-- Contiene los niveles de los cursos
	
CREATE TABLE nivel(
	id INT AUTO_INCREMENT, 
	nombre_nivel VARCHAR(15) NOT NULL, -- Básico, Intermedio, Avanzado
	PRIMARY KEY (id)
	);
	
	DESCRIBE nivel;
	
	SHOW TABLES;
	
-- la dispobilidad horaria para los cursos dictados por los intructores	
CREATE TABLE disponibilidad_horaria(
	id INT AUTO_INCREMENT, 
	dias_de_la_semana VARCHAR(15) NOT NULL,
	hora_inicio TIME NOT NULL,
	hora_fin TIME NOT NULL,
	
	PRIMARY KEY (id)
	);
	
	DESCRIBE disponibilidad_horaria;
	
	SHOW TABLES;
	
-- Guarda los diferentes estilos de baile que ofrece la academia	
CREATE TABLE especialidad_de_baile(
   id INT AUTO_INCREMENT,
   nombre_especialidad_de_baile VARCHAR(20) NOT NULL,
   PRIMARY KEY (id)
   );
	
	DESCRIBE especialidad_de_baile;
	
	SHOW TABLES;
	
-- Contiene los cursos de la acdemia con su informacion 
CREATE TABLE cursos(
	id INT AUTO_INCREMENT, 
	nombre VARCHAR(40) NOT NULL,
	precio_mensual DECIMAL(10,2) NOT NULL,
	codigo VARCHAR(20) UNIQUE NOT NULL,
	cupo_alumnos_max INT (10) NOT NULL,
	id_nivel INT NOT NULL,
	id_especialidad_de_baile INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (id_nivel) REFERENCES nivel(id),
	FOREIGN KEY (id_especialidad_de_baile) REFERENCES especialidad_de_baile(id)
	);
	
	DESCRIBE cursos;
	
	SHOW TABLES;

-- guarda la información de la academia Incluye pagos mensuales y su ID
CREATE TABLE Academia (id INT AUTO_INCREMENT, 
	pagos_mensuales DECIMAL (10) NOT NULL,
	PRIMARY KEY (id),
	id_cursos INT NOT NULL,
	FOREIGN KEY (id_cursos) REFERENCES cursos(id)
	);
	
DESCRIBE Academia;
	
	SHOW TABLES;
	
	
-- Contiene a los estudiantes y su informacion importante para los cursos	
CREATE TABLE estudiantes(
	id INT AUTO_INCREMENT, 
	nombre VARCHAR(100) NOT NULL,
	apellido VARCHAR(40) NOT NULL,
	telefono VARCHAR(10) UNIQUE NOT NULL,
	correo VARCHAR(30) UNIQUE NOT NULL,
	numero_de_documento VARCHAR(10) NOT NULL,
	edad INTEGER(2) NOT NULL,
	id_cursos INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (id_cursos) REFERENCES cursos(id)
	);
	
	DESCRIBE estudiantes;
	
	SHOW TABLES;

	
-- Contiene al instructor de los cursos con su informacion relevante	
CREATE TABLE instructor(
	id INT AUTO_INCREMENT, 
	nombre VARCHAR(100) NOT NULL,
	apellido VARCHAR(40) NOT NULL,
	telefono VARCHAR(10) UNIQUE NOT NULL,
	correo VARCHAR(30) UNIQUE NOT NULL,
	numero_de_documento VARCHAR(10) NOT NULL,
	codigo VARCHAR(10) NOT NULL UNIQUE,
	anos_de_experiencia INTEGER (2) NOT NULL,
	PRIMARY KEY (id),
	id_cursos INT NOT NULL,
	id_disponibilidad_horaria INT NOT NULL,
	FOREIGN KEY (id_cursos) REFERENCES cursos(id),
	FOREIGN KEY (id_disponibilidad_horaria) REFERENCES disponibilidad_horaria(id)
	);
	
	DESCRIBE instructor;
	
	SHOW TABLES;
	
	
-- Guarda los años de experiencia posibles que puede tener un instructor	
CREATE TABLE anos_experiencia(
	id INT AUTO_INCREMENT, 
	años INTEGER(110) NOT NULL,
	id_especialidad_de_baile INT NOT NULL,
	PRIMARY KEY (id),
	FOREIGN KEY (id_especialidad_de_baile) REFERENCES especialidad_de_baile(id)
	);
	
	DESCRIBE anos_experiencia;
	
	SHOW TABLES;
