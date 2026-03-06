# ¿Qué zonas comparten entidad gestora?

## Obtener zonas agrupadas por entidad gestora

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?entidadGestora (GROUP_CONCAT(STR(?zona); SEPARATOR=", ") AS ?zonas)
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:managedBy ?entidadGestora .
}
GROUP BY ?entidadGestora
HAVING (COUNT(?zona) > 1)
ORDER BY ?entidadGestora
```

## Obtener zonas agrupadas por entidad gestora con nombres

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?entidadGestora ?nombreEntidad (GROUP_CONCAT(STR(?zona); SEPARATOR=", ") AS ?zonas)
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:managedBy ?entidadGestora .
    OPTIONAL { ?entidadGestora rdfs:label ?nombreEntidad . }
}
GROUP BY ?entidadGestora ?nombreEntidad
HAVING (COUNT(?zona) > 1)
ORDER BY ?entidadGestora