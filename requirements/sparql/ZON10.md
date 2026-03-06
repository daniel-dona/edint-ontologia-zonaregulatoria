# ¿Cuáles son las zonas de carga y descarga de un municipio concreto?

## Obtener zonas de carga y descarga de un municipio concreto

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?zona
WHERE {
    ?zona rdf:type edintzone:LoadingUnloadingZone ;
          edintzone:locatedIn <URI_DEL_MUNICIPIO> .
}
```

## Obtener zonas de carga y descarga de un municipio concreto con nombres

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?zona ?nombreZona
WHERE {
    ?zona rdf:type edintzone:LoadingUnloadingZone ;
          edintzone:locatedIn <URI_DEL_MUNICIPIO> .
    OPTIONAL { ?zona rdfs:label ?nombreZona . }
}
ORDER BY ?nombreZona