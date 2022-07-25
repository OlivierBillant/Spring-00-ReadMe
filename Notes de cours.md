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

<br>

### Configuation Data minimale

```java
@Entity
public class ClassName
    @Id
    @GeneratedValue
```

Depuis javax.persistence  
Permettra l'ajout en base de donnée d'un objet.

Dans src/main/ressources/Application-properties :

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

<br>

### Les **méthodes DAO** auto-générées :

- A noter que la méthode dao.save gèrera à la fois l'insert et l'update.
- La méthode FindBy rend un optional permettant de gérer les NPE depuis Java8.
  - on pourra alors tester par isEmpty/isPresent l'objet optional
  - la méthode optional.orElse() permet de choisir ce que l'on retournera.
    Exemple :
  ```java
  Contact monContact = dao.findById(0).orElse(null)
  Contact monContact = dao.findById(0).orElse(new Contact(constructor))
  ```
- **JPQL : Création de méthodes par requêtes nommées**  
   Méthode findBy custom : ne sont pas auto-générées comme en Symfony.  
   On utilisera les connecteurs présents ci après :  
   https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation  
   Dans la classe ObjetDao, ajouter :
  ```java
  Objet findByAttribut1AndAttribut2(Type Attribut1, Type Attribut2)
  ```
  Dans l'éventualité ou on veut récupérer des attributs de l'objet et non l'objet en lui-même,  
   on utilisera l'annotation toujours dans la class ObjetDao
  ```java
  @Query("SELECT c.attributCible FROM className c WHERE c.attributSource= :attributSource")
  //Ex
  @Query("SELECT c.tel FROM Contact c WHERE c.prenom= :prenom")
  String getTelByPrenom(@Param("prenom") String prenom)
  ```

<br>

### Relations SQL

On utilisera les annotations de relation type @ManyToOne qui peuvent être assorties  
de paramètres (cascade etc...).  
Les relations seront alors automatiquement créees.  
On pourra ensuite accéder à tous les attributs de l'objet lié.  
Le paramètre **fetch = FetchType.LAZY** pourra prendre deux valeurs :

- LAZY : il fera la requête que si nécessaire (n requêtes si besoin)
- EAGER : il fera la jointure directement et remontera l'ensemble des infos.

### Customisation colonnes et attributs

On peut donner des noms aux entités et tables (paramètre name).  
On peut modifier les modes d'incrémentation des Id.

<br>

### Héritage
Comment gérer l'héritage en db :  
- **One Table** : Une table mère disposera des attributs communs et d'un atrtibut correspodant au type d'une classe fille.  
On optera lorsque l'on a beaucoup d'informations dans l'échelon supérieur.
- **TablePerTable** : recopie des éléments de la classe mère dans les classes filles.
- **Join** Utilisation d'une PK/FK id_classeMere de la classe mère et présente dans les classes filles.  
Nécessitera l'utilisation de jointures pour récupérer l'ensemble des données sans reprt.  
Plus complexe à mettre en place.

Selon l'option prise, la construction des DAO sera largement modifiée.  
Par défaut, la configuration JPA sera OneTable.

### Connexion db
Ajouter dans les dépendances gradle le 
``` java
runtimeOnly 'mysql:mysql-connector-java'
```
Puis dans src/main/ressources modifier application.configuration
``` java
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/db_example
spring.datasource.username=springuser
spring.datasource.password=ThePassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```