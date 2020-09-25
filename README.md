# jakartaee
pratica jakartaee com wildfly e mysql


para este projeto foi utilizado o MySQL, é necessario a seguinte tabela no banco:

CREATE DATABASE agendamentoemaildb;

USE agendamentoemaildb;

CREATE TABLE agendamentoemail (

    id int NOT NULL AUTO_INCREMENT,
    
    email varchar(50) NOT NULL,
    
    assunto varchar(50) NOT NULL,
    
    mensagem varchar(255) NOT NULL,
    
    agendado tinytext NOT NULL,
    
    PRIMARY KEY (id)
    
) 
ENGINE=InnoDB AUTO_INCREMENT=18 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

---------------------------------------

Será necessário o MySQL Connector, se não o possuir faça o download: https://dev.mysql.com/downloads/connector/j/

----------------------------------------

Foi utilizado o servidor de aplicação WildFly, é necessário criar um usuário:

1º - Acesse a pasta wildfly-20.0.1.Final\bin.

2º - Execute, via CMD, o add-user.bat

3º - Escolha o tipo Management User (Usuário de Administração)

4º - Escolha o username de sua preferência

5º - Defina a senha e a confirme

6º - Não é necessário definir grupos, então só é necessário apertar enter

7º - Insira yes para incluir o usuário ao ManagementRealm

8º - Insira yes para permitir que o usuário possa acessar outros AS Process

9º - Tecle qualquer tecla para continuar

OBS: o Username e Senha escolhidos serão necessários para acessar o localhost futuramente.

-----------------------------------------------

Será necessário adicionar o Connector MySQL e criar um datasource. 
Para isto o servidor de aplicação deve estar rodando. 
Digite os seguintes comandos via linha de comando dentro de pasta bin do diretorio de seu wildfly :

jboss-cli.bat (irá iniciar o serviço do jboss dentro de seu terminal, inicialmente estara desconectado, digite "connect")

module add --name=com.mysql --resources="{Local em que o .jar está salvo}" --dependencies=javax.api,javax.transaction.api

/subsystem=datasources/jdbc-driver=mysql:add(driver-name=mysql,driver-module-name=com.mysql,driver-xa-datasource-class-name=com.mysql.cj.jdbc.MysqlXADataSource)


Após executar as linhas de comando acesse pelo navegador o 'localhost:8080', será solicitado o usuario e senha. Logue e siga o caminho -> Subsystems - Datasources & Drivers - DataSources - Add DataSource:
Serão apresentadas 4 paginas para configuração:

1- Selecione MySQL

2- De um Nome para os atributos e para o JNDI, foi utilizado por mim " Name: AgendamentoEmailDS, JNDI Name: java:/AgendamentoEmailDS" ... estes são os nomes nas configurações do projeto em "webapp/WEB-INF/classes/META-INF/persistence.xml", se não pretende alterar utilize os mesmos nomes.

3- Já esta configurado por padrão.

4- Connection URL: jdbc:mysql://localhost:3306/agendamentoemaildb

   User Name e Password são os de seu banco de dados.

--------------------------------------------------------
