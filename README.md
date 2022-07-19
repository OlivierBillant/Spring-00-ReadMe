# Java Avancé - Framework Spring Boot

## Reprise des hostilités : rappels de Java

Spring est un framework (cadre de travail) regroupant un ensemble de
bibliothèques et surtout des modalités de leur utilisation. Considéré
comme un framework à briques on retrouvera ainsi :
- **Core** : 
    - IoC (Inversion of Control) : sous-entend qu'une classe ne pourra
    pas directement instancier une autre classe d'une autre couche. Une classe
    pourra demander à une classe centrale (factory, singleton) la création de classes
    - DI : Injection de Dépendance encadrée par Spring.
    - AOP : Programmation par Aspect correspond à de l'injection de code dans une autre bloc de code sans modifier le code initial.

- **JPA/Hibernate** : 
    - Tous les ORM utilisent la même norme JPA. Attention, les syntaxes pré-JPA sont encore très présentes dans les tutos et ne sont plus utilisables.
    - Spring Data : remplace Spring JDBC et Spring ORM.

- **Front** :
    - Spring MVC + Thymeleaf : analogue des twig en php, remplacera les Servlets/jsp
    - Spring WEB : génération de web services Rest.

- **Gestionnaire de dépendances**
    - Gradle ou Maven. Ici on utilisera Gradle

# Dictionnaire d'annotations
``` java 
@SpringBootApplication  
```
Lanceur principal Spring
``` Java 
@Autowired
private Class classInstance
``` 
Récuprère un @Component, par défaut le @Primary
``` Java 
@Qualifier
``` 
Utilisé avec @Autowired pour récupérer un component par son nom.
``` java 
@Component("componentName")
@Primary
```
Récuprère un @Component, par défaut le @Primary
Un @Component sera automatiquement détecté par @Autowired et pourra être assorti d'un nom.  
Si plusieurs composants, la priorité sera donnée au primary.
