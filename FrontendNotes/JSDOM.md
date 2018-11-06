# JavaScript DOM Notes

## Window vs Document
- **Window**: global obj that holds variables, funcs, history, location
- **Document**: held by window

## HTMLCollection vs NodeList
- **HTMLCollection**: returned by ```getElementsByClassName()``` and ```getElementsByTagName()```, doesn't have ```forEach```
  - ```Array.from()``` to convert into array --> traversable w ```forEach```
- **NodeList**: returned by ```querySelectorAll()```, traversable w ```forEach```
