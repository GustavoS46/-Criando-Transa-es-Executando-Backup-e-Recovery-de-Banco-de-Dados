DELIMITER //

CREATE PROCEDURE vendas_procedure()
BEGIN
    -- Declarar variáveis
    DECLARE exit_handler BOOLEAN DEFAULT FALSE;
    DECLARE rollback_handler BOOLEAN DEFAULT FALSE;
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION SET exit_handler = TRUE;

    -- Desabilitar o autocommit
    SET autocommit = 0;

    -- Iniciar a transação
    START TRANSACTION;

    -- Definir savepoint para rollback parcial (opcional)
    SAVEPOINT savepoint1;

    -- Executar instruções SQL (exemplo)
    INSERT INTO tabela (valor_venda, valor_compra) VALUES (valor1, valor2);
    UPDATE tabela SET valor_venda = novo_valor_venda WHERE condição;
    DELETE FROM tabela WHERE condição;

    -- Para verificar se ocorreu algum erro durante a execução das instruções
    IF exit_handler THEN
        -- Para desfazer o savepoint (rollback parcial) ou desfazer a transação inteira (rollback total)
        IF rollback_handler THEN
            ROLLBACK TO savepoint1;
        ELSE
            ROLLBACK;
        END IF;
    ELSE
        -- Confirmar a transação
        COMMIT;
    END IF;

    -- Reabilitar o autocommit
    SET autocommit = 1;
END //

DELIMITER ;