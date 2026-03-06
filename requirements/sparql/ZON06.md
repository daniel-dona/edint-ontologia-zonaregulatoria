# ¿Cuántas zonas reguladas hay por municipio?

## Contar zonas reguladas por municipio

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?municipio ?tipoZona (COUNT(?zona) AS ?numZonas)
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:locatedIn ?municipio .
}
GROUP BY ?municipio ?tipoZona
ORDER BY ?municipio ?tipoZona
```

## Contar zonas reguladas por municipio con nombres

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?municipio ?nombreMunicipio ?tipoZona (COUNT(?zona) AS ?numZonas)
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:locatedIn ?municipio .
    OPTIONAL { ?municipio rdfs:label ?nombreMunicipio . }
}
GROUP BY ?municipio ?nombreMunicipio ?tipoZona
ORDER BY ?municipio ?tipoZona