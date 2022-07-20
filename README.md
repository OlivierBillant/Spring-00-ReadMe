# Dictionnaire d'annotations

```java
@SpringBootApplication
```

Lanceur principal Spring

```Java
@Autowired
private Class classInstance;
```

Récuprère un @Component, par défaut le @Primary

```Java
@Qualifier
```

Utilisé avec @Autowired pour récupérer un component par son nom.

```java
@Component("componentName")
@Primary
```

Récuprère un @Component, par défaut le @Primary
Un @Component sera automatiquement détecté par @Autowired et pourra être assorti d'un nom.  
Si plusieurs composants, la priorité sera donnée au primary.

## Lombok

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
```

On pense à rajouter l'id de l'objet

```java
@Entity
public class ClassName
    @Id
    @GeneratedValue
```

Depuis javax.persistence

```java
@Query
```
Creation de méthodes par requêtes nommées / Query Methods

```java
@ManyToOne(cascade = CascadeType.PERSIST)
@OneToMany
@ManyToMany
```
Les annotations sont a ajouter sur les attributs que l'on veut lier.  
Les paramètres comme cascade permettront de faciliter les sauvegardes ou les suppressions.