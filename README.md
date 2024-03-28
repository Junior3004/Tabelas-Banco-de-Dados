# LISTA DE TABELAS SQL GENERALISTAS

Com o intuito de agilizar a criação de novas tabelas SQL,
criei essa lista de tabelas comumente usadas em projetos diversos.

No documento contem o nome da tabela e seu respectivo código SQL.

Exemplo:

Usuários (Users)

CREATE TABLE Users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

Espero que seja útil para você, pra mim foi! Vlw

Portfolio:
junioroliveira-dev.com.br

