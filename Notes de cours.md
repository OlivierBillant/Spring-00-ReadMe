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


## Spring Data JPA
### Installation de Lombok

  Ajout de la dépendance dans la configuration du Spring Init
  Lancer Lombok.jar depuis les dépendances du projet pour l'installer.
  Redémarrer Eclipse.

  ### Configuation Data minimale

  ```java
  @Entity
  public class ClassName
      @Id
      @GeneratedValue
  ```

  Depuis javax.persistence
  Permettra l'ajout en base de donnée d'un objet.

  Dans src/main/ressources
  Application properties :

  ```java
      spring.jpa.show-sql=true
      spring.jpa.properties.hibernate.format_sql=true
  ```

  La première affiche les requêtes
  La seconde les formatte.

  Attention, en Spring, les Dao seront appelées Repository.

  Notre Interface contactDao pourra générer automatique les Crud par :

  ```java
  public interface ContactDao extends CrudRepository<Contact, Integer>{}
  ```

  On passe à CrudRepository la classe "Contact" et le type de son Identifiant "Integer"
