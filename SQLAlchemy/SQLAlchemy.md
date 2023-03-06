`SQLALchemy` é um *Object Relational Mapper* para tyrabalhar com banco de dados e Python. Ele possui diferentes ferramentas que podem ser usadas de acordo com as necessidades:

![](https://docs.sqlalchemy.org/en/20/_images/sqla_arch_small.png)

Dessas abordagens, as duas principais são:  **Object Relational Mapper (ORM)** e **Core**.

* Core possui uma ampla integração e serviços de banco de dados da SQLAlchemy. A mais importante sendo a **SQL Expression Language**: um kit de ferramentas independente da ORM, que provê um sistema de construção de expressões SQL compostos por objetos comportos e que podem ser "executados"a um banco de dados de interesse de uma transeção específica. 

> Inserts, updates and deletes (i.e. [DML](https://docs.sqlalchemy.org/en/20/glossary.html#term-DML)) are achieved by passing SQL expression objects representing these statements along with dictionaries that represent parameters to be used with each statement.

* ORM está construido a partir do Core para permitir trabalhar no domínio de objetos de modelos mapeados (*object model mapped*). Quando usando ORM, as consultas SQL s]ao construidas, na maioría das vezes, da mesma forma que no *core*. Contudo, as tarefas de DML, que se referem às questões de persistencia dos dados no banco de dados, são automatizados usando o padrão chamado  [unit of work](https://docs.sqlalchemy.org/en/20/glossary.html#term-unit-of-work). 

Trabalhando com *Core* e *SQL Expression language* represente uma abordagem centrada no Schema (schema-centric) do banco de dados, seguindo um paradigma de programação origentada a imutabilidade. *ORM* está construido em uma abordagtem centrada em domínio (domain-centric) do banco de dados com um paradigma explicitamente orientada ao objeto e  dependente da mutabilidade. 

>Since a relational database is itself a mutable service, the difference is that Core/SQL Expression language is command oriented whereas the ORM is state oriented.

* [[Engine]]
* [[DataBaseCreation]]
* [[TableDeclaration]]
