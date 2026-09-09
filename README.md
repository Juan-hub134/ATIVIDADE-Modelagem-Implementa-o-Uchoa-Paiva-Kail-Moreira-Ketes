# ATIVIDADE-Modelagem-Implementa-o-Uchoa-Paiva-Kail-Moreira-Ketes
Tarefa N1
# Tema: Aluguel de Carros

## Integrantes

* Juan Moreira Morais
* Guilherme Ketes Maia
* Henrick Sousa Uchoa de Carvalho
* Allan Paiva Lopes Filho

## Objetivo Geral

Desenvolver um banco de dados relacional para uma empresa de aluguel de veículos, com foco em motoristas de aplicativos. A proposta é organizar as principais informações relacionadas aos clientes, atendentes, veículos e contratos de aluguel, permitindo um melhor controle das operações realizadas pela empresa. O banco deverá possibilitar o cadastro dos clientes e atendentes, incluindo a possibilidade de um atendente também ser cliente, além do registro dos veículos disponíveis para aluguel, com informações como placa, marca, modelo e tipo de veículo. Também serão armazenadas as informações dos contratos, relacionando o cliente ao veículo alugado e registrando dados como prazo de expiração, data do contrato e forma de pagamento.

## Público-alvo

O banco de dados será desenvolvido para empresas de aluguel de veículos que atendem principalmente motoristas de aplicativos. O foco está em pessoas que utilizam veículos alugados para realizar suas atividades profissionais em plataformas como Uber e 99, facilitando o gerenciamento dos clientes, veículos e contratos de aluguel

## Diagrama do Banco de Dados
![Diagrama do Banco de Dados](/diagrama-corrigido.svg)


## Comandos utilizados na construção do esquema das tabelas de aluguel de veículos

* [SERIAL] Gera automaticamente um número sequencial para o ID - id_cliente, id_veiculo, id_atendente, numero_contrato.
* [PRIMARY KEY] Identifica cada cliente de forma única e não permite repetição - id_cliente, id_veiculo, id_atendente, numero_contrato.
* [VARCHAR] Permite armazenar um nome com N caracteres sem ocupar espaços em branco e ocupando 1-2 bytes para armazenar o tamanho do texto - cpf, nome endereço...
* [NOT NULL] Obriga o preenchimento, evitando que não seja preenchida - cpf, nome, endereço...
* [TEXT] Permite armazenar textos de tamanho variável - endereço, email, marca, modelo, tipo...
* [UNIQUE] Não pode repetir dados - cpf, placa de carro, email...
* [TIMESTAMP] Armazena data e hora juntas - data.
* [DEFAULT] Define um valor padrão caso não envie nenhum dado - data.
* [CURRENT_TIMESTAMP] Armazena a data e a hora de registro de acordo com o servidor - data.
* [id_cliente INT NOT NULL] O vínculo que nesse caso está no contrato - id_cliente INT NOT NULL, id_veiculo INT NOT NULL e id_atendente INT NOT NULL.
* [FOREING KEY] Bloqueia a possibilidade de contratos não associados a um cliente, atendente e veículo já existentes e também para impedir exclusão de dados já associados - fk_contrato_cliente, fk_contrato_veiculo e fk_contrato_atendente.


## Tabela de clientes
```sql
 CREATE TABLE cliente (
    id_cliente SERIAL PRIMARY KEY,
    cpf VARCHAR(14) UNIQUE  NOT NULL,
    nome VARCHAR(20) NOT NULL,
    sobrenome VARCHAR(50) NOT NULL,
    endereco TEXT NOT NULL,
    dados_bancarios TEXT UNIQUE NOT NULL,
    email TEXT UNIQUE NOT NULL
	);
```
## Tabela de Veículos 
```sql
CREATE TABLE veiculo (
    id_veiculo SERIAL PRIMARY KEY,
    placa VARCHAR(7) UNIQUE NOT NULL,
    marca TEXT NOT NULL,
    modelo TEXT NOT NULL,
    tipo TEXT NOT NULL 
	);
```
## Tabela de Atendentes
```sql
CREATE TABLE atendente (
    id_atendente SERIAL PRIMARY KEY,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    nome VARCHAR(20) NOT NULL,
    sobrenome VARCHAR(50) NOT NULL,
    endereco TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
	Ativo BOOLEAN DEFAULT TRUE
	);
```
## Contrato 
```sql
CREATE TABLE contrato (
    numero_contrato SERIAL PRIMARY KEY,
    data TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    tipo_pagamento TEXT NOT NULL,
    inicio_vigencia DATE NOT NULL,
    fim_vigencia DATE NOT NULL,
    id_cliente INT NOT NULL,
    id_veiculo INT NOT NULL,
	id_atendente INT NOT NULL,
	CONSTRAINT fk_contrato_cliente FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente),
    CONSTRAINT fk_contrato_veiculo FOREIGN KEY (id_veiculo) REFERENCES veiculo(id_veiculo),
	CONSTRAINT fk_contrato_atendente FOREIGN KEY (id_atendente) REFERENCIES atendente(id_atendente)
	);
```
##  COMANDOS PARA INSERIR DADOS
```sql
	INSERT INTO cliente (cpf, nome, sobrenome, endereco, dados_bancarios, email)
	VALUES
	('111.222.333-01', 'João', 'Silva', 'Rua das Flores, 120', 'Banco 001 - Conta 12345-6', 'joao.silva@email.com'),
	('222.333.444-02', 'Maria', 'Santos', 'Avenida Brasil, 450', 'Banco 002 - Conta 23456-7', 'maria.santos@email.com'),
	('333.444.555-03', 'Carlos', 'Oliveira', 'Rua Central, 85', 'Banco 003 - Conta 34567-8', 'carlos.oliveira@email.com'),
	('444.555.666-04', 'Ana', 'Costa', 'Rua do Comércio, 310', 'Banco 004 - Conta 45678-9', 'ana.costa@email.com'),
	('555.666.777-05', 'Pedro', 'Almeida', 'Avenida Norte, 720', 'Banco 005 - Conta 56789-0', 'pedro.almeida@email.com'); 

	INSERT DOS VEICULOS

	INSERT INTO veiculo (placa, marca, modelo, tipo)
	VALUES
	('ABC1D23', 'Toyota', 'Corolla', 'Sedan'),
	('DEF4E56', 'Honda', 'Civic', 'Sedan'),
	('GHI7F89', 'Volkswagen', 'T-Cross', 'SUV'),
	('JKL0G12', 'Chevrolet', 'Onix', 'Hatch'),
	('MNO3H45', 'Fiat', 'Strada', 'Pickup');

	INSERT DOS ATENDENTES

	INSERT INTO atendente (cpf, nome, sobrenome, endereco, email)
	VALUES
	('666.777.888-06', 'Lucas', 'Ferreira', 'Rua das Palmeiras, 100', 'lucas.ferreira@empresa.com'),
	('777.888.999-07', 'Juliana', 'Martins', 'Avenida Central, 250', 'juliana.martins@empresa.com'),
	('888.999.000-08', 'Rafael', 'Souza', 'Rua Amazonas, 430', 'rafael.souza@empresa.com'),
	('999.000.111-09', 'Beatriz', 'Rodrigues', 'Rua Principal, 560', 'beatriz.rodrigues@empresa.com');

	INSERT DO CONTRATO

	INSERT INTO contrato 
    (tipo_pagamento, inicio_vigencia, fim_vigencia, id_cliente, id_veiculo, id_atendente)
    VALUES
    ('Cartão de crédito', '2026-01-10', '2026-02-10', 1, 1, 1),
    ('Pix',               '2026-02-15', '2026-03-15', 2, 2, 2),
    ('Cartão de débito',  '2026-03-01', '2026-04-01', 3, 3, 3),
    ('Dinheiro',          '2026-04-05', '2026-05-05', 4, 4, 4),
    ('Cartão de crédito', '2026-05-10', '2026-06-10', 5, 5, 1),
    ('Pix',               '2026-06-15', '2026-07-15', 1, 3, 2),
    ('Cartão de crédito', '2026-07-20', '2026-08-20', 2, 4, 3);

```
## IMAGENS REFERENTES AO pgAdmin 4 

