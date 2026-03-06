# ¿Cuáles son las zonas de estacionamiento y sus horarios?

## Obtener zonas de aparcamiento y sus horarios

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?zona ?tipo ?horario
WHERE {
    ?zona rdf:type ?tipo .
    ?tipo rdfs:subClassOf* edintzone:RegulatedParkingZone .
    OPTIONAL { ?zona edintzone:scheduleDescription ?horario . }
}
ORDER BY ?tipo ?zona ?horario
```

## Obtener zonas de aparcamiento con ubicación

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?zona ?tipo ?municipio ?horario
WHERE {
    ?zona rdf:type ?tipo .
    ?tipo rdfs:subClassOf* edintzone:RegulatedParkingZone .
    OPTIONAL { ?zona edintzone:scheduleDescription ?horario . }
    OPTIONAL { ?zona edintzone:locatedIn ?municipio . }
}
ORDER BY ?tipo ?zona ?horario
```

## Obtener zonas de aparcamiento con nombres y fechas de validez

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?zona ?tipo ?nombreZona ?municipio ?nombreMunicipio ?horario ?fechaInicio ?fechaFin
WHERE {
    ?zona rdf:type ?tipo .
    ?tipo rdfs:subClassOf* edintzone:RegulatedParkingZone .
    OPTIONAL { ?zona rdfs:label ?nombreZona . }
    OPTIONAL { ?zona edintzone:locatedIn ?municipio . }
    OPTIONAL { ?municipio rdfs:label ?nombreMunicipio . }
    OPTIONAL { ?zona edintzone:scheduleDescription ?horario . }
    OPTIONAL { ?zona edintzone:startDate ?fechaInicio . }
    OPTIONAL { ?zona edintzone:endDate ?fechaFin . }
    FILTER (!BOUND(?nombreZona) || lang(?nombreZona) = "" || lang(?nombreZona) = "es")
    FILTER (!BOUND(?nombreMunicipio) || lang(?nombreMunicipio) = "" || lang(?nombreMunicipio) = "es")
}
ORDER BY ?tipo ?zona ?horario