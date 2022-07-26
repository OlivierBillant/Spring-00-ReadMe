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
@OneToMany(mappedBy = "candidat")
@ToString.Exclude
@ManyToMany(cascade = CascadeType.PERSIST)
```

Les annotations sont a ajouter sur les attributs que l'on veut lier.  
Les paramètres comme cascade permettront de faciliter les sauvegardes ou les suppressions.
On retrouvera ainsi mappedBy qui permettra d'associer précisément deux tables entre elles.
Le ToString.Exclude permettra d'éviter les Overflow lors de l'affichage d'instances.

```java
@Table(name = "candidate")
```

Pour changer un nom de table.

```java
@Inheritance(strategy = InheritanceType.SINGLE_TABLE) // .JOINED .TABLE_PER_CLASS
@DiscriminatorColumn(name = "ty_entreprise", length = 5)
@DiscriminatorValue("ENT")
```

Pour définir le mode d'héritage. par défault SINGLE_TABLE.  
Les discriminators seront utiles dans ce cas uniquement.

```java
@RestController
```

Définit la classe en composant controller Rest.

```java
@RequestMapping("/path")
public class ClassName{
    @GetMapping(/path/{arg})
    @GetMapping("/hello/{lang}")
	public String disHello2(@PathVariable("lang") String lang) {}

    @GetMapping("")
    public ArrayList<Objet> afficherTout() {
        return objetManager.findAll();
    }

    @GetMapping("/{id}")
    public Objet objet afficherUn(@RequestBody Integer id) {
        return objetManager.findById(id);
    }

    @DeleteMapping("/{id}")
    public void effacer(@PathVariable("id") Integer id) {}

    @PostMapping("")
    public void ajouter(@RequestBody Objet objet) {
            objetManager.addObjet(objet);
        }
}
    @PutMapping("")
	public void modifier(@RequestBody Objet objet) {
		objetManager.editObjet(objet);
	}
}
```

@RequestMapping définira le chemin par défaut.
Les Get/DeleteMapping permettent de définir les méthodes utilisées.

```java
@JSONIgnore
@JsonIdentityInfo(generator = ObjectIdGenerators.PropertyGenerator.class,
                    property = "id")
```
Pour éviter les doubles dépendances en JSON. JSON ignore entraine une perte d'information.  
Alternativement on peut utiliser le second qui va se baser sur les identifiant donné pour éviter les doublons.

```java
@Transactional
```
Dans tous les managers.