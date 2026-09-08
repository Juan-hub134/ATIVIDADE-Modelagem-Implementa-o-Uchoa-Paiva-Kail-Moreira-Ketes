# ATIVIDADE-Modelagem-Implementa-o-Uchoa-Paiva-Kail-Moreira-Ketes
Tarefa N1
# Tema: Aluguel de Carros

## Integrantes

* Juan Moreira
* Guilherme Ketes Maia
* Henrick Uchoa
* Alan Paiva

## Objetivo Geral

Desenvolver um banco de dados relacional para uma empresa de aluguel de veículos, com foco em motoristas de aplicativos. A proposta é organizar as principais informações relacionadas aos clientes, atendentes, veículos e contratos de aluguel, permitindo um melhor controle das operações realizadas pela empresa. O banco deverá possibilitar o cadastro dos clientes e atendentes, incluindo a possibilidade de um atendente também ser cliente, além do registro dos veículos disponíveis para aluguel, com informações como placa, marca, modelo e tipo de veículo. Também serão armazenadas as informações dos contratos, relacionando o cliente ao veículo alugado e registrando dados como prazo de expiração, data do contrato e forma de pagamento.

## Público-alvo

O banco de dados será desenvolvido para empresas de aluguel de veículos que atendem principalmente motoristas de aplicativos. O foco está em pessoas que utilizam veículos alugados para realizar suas atividades profissionais em plataformas como Uber e 99, facilitando o gerenciamento dos clientes, veículos e contratos de aluguel

## Diagrama do Banco de Dados
![Diagrama do Banco de Dados](./diagrama-tarefaN1.svg)


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
-- Tabela para armazenar os dados de cadastro de clientes

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
-- Tabela que armazena dados de veiculos cadastrados

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
-- Tabela que armazena dados dos atendentes e se estao ativos na empresa de alguel de carros

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
-- Tabela que armazena dados dos contratos de aluguel de veiculos e referencia a clientes, veiculos e atendentes

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
