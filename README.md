# Projeto: Banco de Dados para Gestão Veterinária (PostgreSQL)

Este repositório contém o esquema de banco de dados desenvolvido para a gestão técnica de uma clínica. O projeto demonstra a aplicação de conceitos de banco de dados relacionais, normalização e integridade referencial.

## 📊 Diagrama de Dados
![Diagrama do Banco de Dados](./diagrama.png)
*Diagrama Entidade-Relacionamento representando a lógica do sistema.*

## 📋 Dicionário de Dados e Regras de Negócio

| Tabela | Função | Chave Estrangeira (FK) | Comportamento ON DELETE |
| :--- | :--- | :--- | :--- |
| **Endereco** | Cadastro de Localidades (Logradouros). | -- | -- |
| **Veterinarios** | Dados do corpo clínico. | `id_end` | **SET NULL** |
| **Cliente_Tutor**| Cadastro de responsáveis. | `id_end` | **SET NULL** |
| **Paciente** | Dados biológicos do animal. | `id_tutor` | **RESTRICT** |
| **Consulta** | Intersecção (Evento clínico). | `id_animal`, `id_vet`| **RESTRICT** |


## 🔍 Demonstração de Consultas Técnicas

Como tomador de decisão baseado em dados, estruturei consultas para extrair informações vitais para a operação:

### 1. Cruzamento de Dados (JOIN)
Esta consulta une a tabela de animais aos seus respectivos proprietários e histórico de consultas. É fundamental para identificar a quem pertence cada paciente em um relatório de agendamento:

```sql
SELECT 
    p.nome AS proprietario, 
    a.nome AS paciente_animal, 
    a.especie, 
    c.data_consulta
FROM proprietarios p
JOIN animais a ON p.id = a.proprietario_id
JOIN consultas c ON a.id = c.animal_id
ORDER BY c.data_consulta DESC;
```

###2. Filtragem de dados (WHERE)

```SELECT nome, raca, data_nascimento
FROM animais
WHERE especie = 'Felino'
AND status = 'Ativo';
```

## 🎯 Objetivo
Desenvolver uma estrutura de dados robusta para suporte à decisão clínica, unindo minha experiência na medicina veterinária com as melhores práticas de engenharia de software.

## 🧠 Desafios e Expectativas
O maior desafio foi modelar a relação N:N (Muitos para Muitos) entre Procedimentos e Consultas. Espero que este projeto demonstre minha capacidade de transpor regras de negócio complexas para um modelo lógico eficiente.

## 📂 Conteúdo do Banco
- **Cadastro de Clientes:** Gestão de contatos e endereços.
- **Prontuário Digital:** Histórico de espécies, raças e idades.
- **Controle de Consultas:** Datas, diagnósticos e observações técnicas.


⚠️ Nota sobre Segurança: Este projeto utiliza dados fictícios para fins de demonstração. Em um ambiente de produção, os dados dos proprietários (CPF, Telefone) seriam tratados seguindo os protocolos da LGPD para garantir a privacidade dos clientes.

