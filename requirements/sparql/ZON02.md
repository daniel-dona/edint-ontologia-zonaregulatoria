# ¿Cuál es el municipio de cada zona de bajas emisiones?

## Obtener municipio de cada zona de bajas emisiones

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX esadm: <http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT ?zbe ?municipio
WHERE {
    ?zbe rdf:type edintzone:LowEmissionZone ;
         edintzone:locatedIn ?municipio .
}
ORDER BY ?zbe
```

## Obtener municipio con su nombre

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX esadm: <http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?zbe ?municipio ?nombreMunicipio
WHERE {
    ?zbe rdf:type edintzone:LowEmissionZone ;
         edintzone:locatedIn ?municipio .
    ?municipio rdfs:label ?nombreMunicipio .
}
ORDER BY ?zbe ?nombreMunicipio
```

## Obtener municipio con nombres en español

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX esadm: <http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?zbe ?municipio ?nombreMunicipio
WHERE {
    ?zbe rdf:type edintzone:LowEmissionZone ;
         edintzone:locatedIn ?municipio .
    ?municipio rdfs:label ?nombreMunicipio .
    FILTER (lang(?nombreMunicipio) = "" || lang(?nombreMunicipio) = "es")
}
ORDER BY ?zbe ?nombreMunicipio
```

## Obtener municipio con fechas de validez

```sparql
PREFIX edintzone: <http://vocab.linkeddata.es/datosabiertos/def/common/zone#>
PREFIX esadm: <http://vocab.linkeddata.es/datosabiertos/def/sector-publico/territorio#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?zbe ?municipio ?nombreMunicipio ?inicio ?fin
WHERE {
    ?zbe rdf:type edintzone:LowEmissionZone ;
         edintzone:locatedIn ?municipio .
    ?municipio rdfs:label ?nombreMunicipio .
    FILTER (lang(?nombreMunicipio) = "" || lang(?nombreMunicipio) = "es")
    OPTIONAL { ?zbe edintzone:startDate ?inicio . }
    OPTIONAL { ?zbe edintzone:endDate ?fin . }
    FILTER (
        (!BOUND(?inicio) || xsd:date(?inicio) <= xsd:date(NOW()))
        &&
        (!BOUND(?fin) || xsd:date(?fin) >= xsd:date(NOW()))
    )
}
ORDER BY ?zbe ?nombreMunicipio