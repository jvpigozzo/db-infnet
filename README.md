# Principais Ferramentas para Gerencias Banco de Dados

#### Código fonte do exemplo prático apresentado durante a aula 'Principais ferramentas para gerenciar bancos de dados.' ministrada no minicurso de Engenharia de Dados do Infnet.

## Instalação do PostgreSQL

Siga o passo a passo apresentado em aula para instalar e configurar o PostgreSQL. Finalizada a instalação e configuração utilize os comandos a seguir para criar as tabelas no banco de dados `FLUXOFINANCEIRO`:


``` SQL
-- Criar tabela de clientes
CREATE TABLE clientes (
    cliente_id SERIAL PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(14) UNIQUE NOT NULL,
    endereco VARCHAR(255),
    telefone VARCHAR(20)
);

-- Criar tabela de contas
CREATE TABLE contas (
    conta_id SERIAL PRIMARY KEY,
    cliente_id INT REFERENCES clientes(cliente_id),
    tipo_conta VARCHAR(20) NOT NULL,
    saldo DECIMAL(15, 2) DEFAULT 0.0
);

-- Criar tabela de transações
CREATE TABLE transacoes (
    transacao_id SERIAL PRIMARY KEY,
    conta_id INT REFERENCES contas(conta_id),
    tipo_transacao VARCHAR(20) NOT NULL,
    valor DECIMAL(15, 2) NOT NULL,
    data_transacao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Execute a consulta acima para criar as tabelas e em seguida utilize o comando `INSERT` para popular as tabelas criadas com dados:

``` SQL
-- Inserir dados na tabela de clientes
INSERT INTO clientes (nome, cpf, endereco, telefone) VALUES
    ('João Silva', '123.456.789-01', 'Rua A, 123', '(11) 98765-4321'),
    ('Maria Oliveira', '987.654.321-09', 'Avenida B, 456', '(21) 98765-4321'),
    ('Carlos Santos', '111.222.333-44', 'Travessa C, 789', '(31) 98765-4321');

-- Inserir dados na tabela de contas
INSERT INTO contas (cliente_id, tipo_conta, saldo) VALUES
    (1, 'Corrente', 5000.00),
    (2, 'Poupança', 10000.00),
    (3, 'Corrente', 2000.00);

-- Inserir dados na tabela de transações
INSERT INTO transacoes (conta_id, tipo_transacao, valor) VALUES
    (1, 'Depósito', 1000.00),
    (2, 'Saque', 500.00),
    (3, 'Depósito', 200.00),
    (1, 'Transferência', -300.00),
    (2, 'Transferência', -1000.00),
    (3, 'Saque', 50.00);```
```
