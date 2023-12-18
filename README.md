# Data Wanderings

Data Wanderings is an audiovisual installation created as part of Polifonia, a research project funded by the Europe Horizon 2020 program.

## Creation process

### 1. Data extraction

Data wanderings uses data extracted from the [Choco](https://github.com/smashub/choco) database.
Specifically, a collection of 20861 records representing the chord sequences played in songs analyzed in the context of the Polifonia project. The data is divided in csv files of 2000 records and available in the folder `choco_data--chords`.

The data has been extracted using queries like:

```
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX jams: <http://w3id.org/polifonia/ontology/jams/>
PREFIX mm: <http://w3id.org/polifonia/ontology/music-entity/>
PREFIX core: <http://w3id.org/polifonia/ontology/core/>

SELECT DISTINCT ?title ?musicentity ?observationValue ?startTime ?startTimeType ?duration ?durationType
WHERE {
  ?musicentity a mm:MusicEntity ;
    core:title ?title ;
    jams:hasJAMSAnnotation ?annotation .
  ?annotation jams:includesObservation ?observation ;
    jams:hasAnnotationType "chord" .
  ?observation rdfs:label ?observationValue ;
    jams:hasMusicTimeInterval [jams:hasMusicTimeDuration [ jams:hasValue ?duration ; jams:hasValueType ?durationType ] ;
      jams:hasMusicTimeStartIndex [ jams:hasMusicTimeIndexComponent [ jams:hasValue ?startTime ; jams:hasValueType ?startTimeType  ]]] .
}
ORDER BY ?title ?startTime
LIMIT 1000
OFFSET 0
```

### 2. Data manipulation

The file `chords_notes_frequencies.tsv` contains corrispondences of chords with notes and sound frequencies.

### 3. Data utilization


## More info

The sensory journey “Data Wanderings” is a new project of Polifonia. The art installation has been open from Oct. 13 to 28, 2023 in Bologna, Italy.

‘Data Wanderings’ is a synaesthetic installation that challenges the boundaries between art and technology by transforming the rawness of data into a memorable sensorial journey. The audiovisual installation was conceived with the aim of making the user experience a physical simulation of virtual interaction with the mass of data coming from the knowledge graph of the “Polifonia” project.
Data Wanderings invites viewers to embark on a journey through the intricate labyrinth of data, to discover the secret melodies of numbers, and to embrace the creative and informative potential that lies within them.
The Choco database of Polifonia collects data on chords extracted from a series of songs. All song chords are listed in time sequence in a table, converted into a series of notes and their sound frequencies.
In the interactive installation, the eight frequencies of each chord are translated directly into pixels and they create eight mixed patterns to obtain the final “visual noise” patterns.
The frequencies also produce a generative soundtrack through FM synthesis to create a crazy digital [Orchestrion](https://en.wikipedia.org/wiki/Orchestrion).
The sphere floating in the center of the screen acts as an interface with visitors and it is generated using the album and singles’ covers from which the chord data was derived. People’s movements are detected with a camera, analyzed and used to influence images and sound by controlling a low-pass filter.

## Credits

Art Direction: Umanesimo Artificiale
Concept: Filippo Rosati, Alex Piacentini
Data Analysis: Alex Piacentini, Andrea Poltronieri, Jacopo de Berardinis
Creative Coding: Alex Piacentini
Sound Design: Alex Piacentini
edited by: Federica Patti
a POLIFONIA project
