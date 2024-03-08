PARTE 1 – Criando Transações

-- Desabilitar o autocommit
SET autocommit = 0;

-- Iniciar a transação
START TRANSACTION;

-- Executar instruções SQL (exemplo)
/* 
   INSERT INTO tabela (coluna1, coluna2) VALUES (valor1, valor2);
   UPDATE tabela SET coluna1 = novo_valor WHERE condição;
*/

-- Confirmar a transação
COMMIT;

-- Desfazer a transação (rollback) em caso de erro
/* 
   ROLLBACK;
*/

-- Reabilitar o autocommit
SET autocommit = 1;