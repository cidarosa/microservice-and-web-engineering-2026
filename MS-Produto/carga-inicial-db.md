# Microsserviço Produtos
## Carga Inicial no Banco de Dados para Testes

File: `src/main/resources/import.sql`

```sql
INSERT INTO tb_categoria(nome) VALUES('Smartphone');
INSERT INTO tb_categoria(nome) VALUES('Smart TV');
INSERT INTO tb_categoria(nome) VALUES('Notebook');
INSERT INTO tb_categoria(nome) VALUES('Tablet');
INSERT INTO tb_categoria(nome) VALUES('Mouse');
INSERT INTO tb_categoria(nome) VALUES('Teclado');

INSERT INTO tb_loja (nome, email) VALUES ('Americanas', 'center.norte@americanas.com');
INSERT INTO tb_loja (nome, email) VALUES ('Fast Shop', 'loja.tatuape@fast.com.br');
INSERT INTO tb_loja (nome, email) VALUES ('Magazine Luiza', 'taubate@magalu.com.br');
INSERT INTO tb_loja (nome, email) VALUES ('Submarino', 'vendas@submarino.com');

INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Smart TV', 'Smart TV LG LED 50 polegadas', 2285.0, 2);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Mouse Microsoft', 'Mouse sem fio', 250.0, 5);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Teclado Microsoft', 'Teclado sem fio', 278.95, 6);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Smartphone Samsung Galaxy A54 5G', 'Samsung Galaxy A54 5G', 1799.0, 1);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Smart TV', 'Samsung Vision AI TV 85" QLED Ultra 4K Q7F 2025', 8799, 2);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Teclado Logitech', 'Teclado sem fio', 358.0, 6);
INSERT INTO tb_produto (nome, descricao, valor, categoria_id) VALUES ('Apple iPhone 17', 'Apple iPhone 17, 256G, Azul Névoa', 7999.00, 1);

INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (1, 1);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (1, 3);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (2, 1);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (2, 4);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (3, 2);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (4, 2);
INSERT INTO tb_produto_loja (produto_id, loja_id) VALUES (5, 2);
```