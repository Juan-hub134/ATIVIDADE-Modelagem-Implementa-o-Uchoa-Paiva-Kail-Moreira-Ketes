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


## Tabela de Cliente
 CREATE TABLE cliente (
     id_cliente SERIAL PRIMARY KEY,
     cpf VARCHAR(14) NOT NULL,
     nome VARCHAR(20) NOT NULL,
     sobrenome VARCHAR(50) NOT NULL,
     endereco TEXT NOT NULL,
     dados_bancarios TEXT NOT NULL,
     email TEXT NOT NULL
  	);
