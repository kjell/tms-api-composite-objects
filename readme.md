Four examples of where we're using a 'composite' image to refer to
multiple TMS objects.

How can we connect these images to their depicted objects in TMS?

Ideally, it would be simple to refer to TMS metadata about each of these
images that depict more than a single 'object'.  Whether that's by
creating a record in TMS that comprises multiple objects or a method on
our API that could "merge" metadata for the objects, I'm not quite sure
yet.

| object | accession numbers | image | object meta |
| ---  | --- | --- | --- |
| Rice Cultivation | `81.1.1-16` | ![](http://cdn.dx.artsmia.org/thumbs/tn_rice-cultivation-wide.jpg) | [22412 31445 95013 95014 95015 96529 96530 96531 96532 96533 96534 96535 96536 96537 96538 96539 96540](./rice-cultivation/) |
| Tale of Genji | `2013.29.14.1-2` | ![](http://cdn.dx.artsmia.org/thumbs/tn_genji-stacked2.jpg) | [117152 117153](./genji/) |
| Leda + Ganymede | `78.63.1-2` | ![](http://cdn.dx.artsmia.org/thumbs/tn_mia_33788a.jpg) | [2560 2561](./montauti/) |
| Duluth Living Room | `G320`** | ![](http://cdn.dx.artsmia.org/thumbs/tn_mia_25304a.jpg) | [10016 10042 23139 23273 23274 23376 23377 23402 23423 23441 23442 23449 8363](./prindle-room/) |

** For the Prindle room, we're using gallery number instead of accession number which is a kludge.

# TMS 'virtual' objects

There are lots of types of these that Frances is working on with the TMS data
standardization group.

* an object made up of component parts
* a 'virtual object' made up of other objects
* a 'see also' link between two (or more??) objects
* 'physically same, intellectually different': something like a painting
  with an unrelated sketch on the back, a sheet with two drawings, a
  sketchbook…

Do these objects fit into any of the above types?

# 'Building' metadata for more than one object

If we could associate multiple object IDs with any given image, we could
build a 'metadata combiner'. It would take multiple object IDs and
combine their metadata somehow. It could take common fields, discarding
differences.

Given [2560](./montauti/2560.json) and [2561](./montauti/2561.json),
we could get output that looked like

```json
{
  "artist": "Antonio Montauti",
  "continent": "Europe",
  "country": "Italy",
  "creditline": "The Putnam Dana McMillan Fund",
  "culture": null,
  "dated": "c. 1710",
  "life_date": "Italian, 1683-1746",
  "marks": " ",
  "medium": "Bronze",
  "nationality": "Italian",
  "provenance": "",
  "restricted": 0,
  "role": "Artist",
  "room": "G310",
  "style": "18th century",
}
```

That might not be that useful, but is it better than nothing?

[117152](./genji/117152.json) and [117153](./genji/117153.json) looks
a lot less useful

```json
{
  "creditline": "Gift of the Clark Center for Japanese Art & Culture",
  "culture": "Japanese",
  "dated": "mid-17th century",
  "life_date": null,
  "marks": " ",
  "nationality": null,
  "provenance": "",
  "restricted": 0,
  "role": "Artist",
  "room": "Not on View",
  "style": "17th century",
}
```

We could also "combine" certain fields. Here `accession_number` and `title`:

```json
{
  "accession_number": "78.63.1-2",
  "artist": "Antonio Montauti",
  "continent": "Europe",
  "country": "Italy",
  "creditline": "The Putnam Dana McMillan Fund",
  "culture": null,
  "dated": "c. 1710",
  "life_date": "Italian, 1683-1746",
  "marks": " ",
  "medium": "Bronze",
  "nationality": "Italian",
  "provenance": "",
  "restricted": 0,
  "role": "Artist",
  "room": "G310",
  "style": "18th century",
  "title": "Leda and the Swan and Ganymede and the Eagle"
}
```

This is pretty much the exact metadata I want in the composite
object
