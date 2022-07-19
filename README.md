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
