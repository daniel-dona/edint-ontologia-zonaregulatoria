# ¿Cuáles son los horarios de funcionamiento o la programación de la regulación?

## Obtener horarios de funcionamiento o programación de la regulación

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?zona ?tipoZona ?horario
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:scheduleDescription ?horario .
}
ORDER BY ?tipoZona ?zona ?horario
```

## Obtener horarios de funcionamiento con nombres de zona

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?zona ?tipoZona ?nombreZona ?horario
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:scheduleDescription ?horario .
    OPTIONAL { ?zona rdfs:label ?nombreZona . }
}
ORDER BY ?tipoZona ?zona ?horario
```

## Obtener horarios de funcionamiento con filtro de nombre en español

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?zona ?tipoZona ?nombreZona ?horario
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:scheduleDescription ?horario .
    OPTIONAL { ?zona rdfs:label ?nombreZona . }
    FILTER (!BOUND(?nombreZona) || lang(?nombreZona) = "" || lang(?nombreZona) = "es")
}
ORDER BY ?tipoZona ?zona ?horario
```

## Obtener horarios de funcionamiento con fechas de validez

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?zona ?tipoZona ?nombreZona ?horario ?fechaInicio ?fechaFin
WHERE {
    ?zona rdf:type ?tipoZona .
    ?tipoZona rdfs:subClassOf* edintzone:RegulatedZone .
    ?zona edintzone:scheduleDescription ?horario .
    OPTIONAL { ?zona rdfs:label ?nombreZona . }
    OPTIONAL { ?zona edintzone:startDate ?fechaInicio . }
    OPTIONAL { ?zona edintzone:endDate ?fechaFin . }
}
ORDER BY ?tipoZona ?zona ?horario