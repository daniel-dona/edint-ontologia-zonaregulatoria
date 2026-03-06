# ¿Cuáles son las zonas reguladas?

## Listar todas las zonas reguladas

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?zona
WHERE {
    ?zona rdf:type edintzone:RegulatedZone .
}
```

## Listar todas las zonas reguladas incluyendo subclases

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?zona
WHERE {
    ?zona rdf:type ?tipo .
    ?tipo rdfs:subClassOf* edintzone:RegulatedZone .
}
ORDER BY ?zona
```

## Listar zonas con sus tipos específicos

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?zona ?tipo ?nombre
WHERE {
    ?zona rdf:type ?tipo .
    ?tipo rdfs:subClassOf* edintzone:RegulatedZone .
    OPTIONAL { ?zona rdfs:label ?nombre . }
}
ORDER BY ?tipo ?zona