# ¿Qué calles específicas componen una zona regulada?

## Obtener calles que componen una zona regulada

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>

SELECT ?zona ?tipoZona ?calle
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:composedOf ?calle .
}
ORDER BY ?tipoZona ?zona ?calle
```

## Obtener calles que componen una zona regulada con nombres de calle

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>

SELECT ?zona ?tipoZona ?calle ?nombreCalle
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:composedOf ?calle .
    OPTIONAL { ?calle rdfs:label ?nombreCalle . }
}
ORDER BY ?tipoZona ?zona ?nombreCalle
```

## Obtener calles con información adicional

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>

SELECT ?zona ?tipoZona ?calle ?nombreCalle ?geometria
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:composedOf ?calle .
    OPTIONAL { ?calle rdfs:label ?nombreCalle . }
    OPTIONAL {
        ?calle geo:hasGeometry ?geoCalle .
        ?geoCalle geo:asWKT ?geometria .
    }
}
ORDER BY ?tipoZona ?zona ?nombreCalle
```

## Obtener calles con filtro de nombre en español

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?zona ?tipoZona ?calle ?nombreCalle
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:composedOf ?calle .
    OPTIONAL { ?calle rdfs:label ?nombreCalle . }
    FILTER (!BOUND(?nombreCalle) || lang(?nombreCalle) = "" || lang(?nombreCalle) = "es")
}
ORDER BY ?tipoZona ?zona ?nombreCalle