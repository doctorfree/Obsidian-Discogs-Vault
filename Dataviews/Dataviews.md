---
banner: "assets/banners/Dataview-Banner.png"
banner_x: 1.0
banner_y: 1.0
---

# Dataviews

The Obsidian Discogs Vault markdown contains metadata with tags allowing a variety of queries using the [Dataview](https://blacksmithgu.github.io/obsidian-dataview/) plugin for [Obsidian](https://obsidian.md/). A few example Dataview queries are detailed below.

## Example Dataview Queries

- [Discogs_Albums](Discogs_Albums.md)
- [Discogs_Albums_1977](Discogs_Albums_1977.md)
- [Discogs_Albums_70s](Discogs_Albums_70s.md)
- [Discogs_Art_Rock](Discogs_Art_Rock.md)
- [Discogs_Progressive](Discogs_Progressive.md)
- [Discogs_Reissue](Discogs_Reissue.md)

## Example Dataview Discogs Query

The markdown for "Fragile" by Yes has the following YAML prelude:

```yaml
---
title: Fragile
artist: Yes
label: Atlantic
formats: Vinyl, LP, Album, Reissue
genres: Rock, Prog Rock, Art Rock, Symphonic Rock
rating: 4.7
released: 2016-05-13
year: 1971
releaseid: 8515237
mediacondition: 
sleevecondition: 
speed: 
weight: 
notes: 
---
```

### Dataview Discogs query

The above album metadata can be used to perform Dataview queries to search, filter, and retrieve albums as if they are in a database. For example, to produce a table of all albums in this vault by Yes released prior to 1980 add the following to a markdown file in the vault:

````markdown
```dataview
TABLE WITHOUT ID
  link(file.link, album) as Album,
  artist AS "Artist",
  year AS "Year"
FROM "Doctorfree"
WHERE artist = "Yes" and year < 1980
SORT year ASC
```
````

The above Dataview code block produces the following output:

```dataview
TABLE WITHOUT ID
  link(file.link, album) as Album,
  artist AS "Artist",
  year AS "Year"
FROM "Doctorfree"
WHERE artist = "Yes" and year < 1980
SORT year ASC
```

As a list grouped by artist rather than a table, the following dataview codeblock:

````markdown
```dataview
LIST link(rows.file.link, rows.album)
FROM "Doctorfree"
WHERE (artist = "Yes" OR artist = "XTC") AND
      year < 1990
GROUP BY "**" + artist + "**"
```
````

Would list all albums by Yes or XTC released prior to 1990:

```dataview
LIST link(rows.file.link, rows.album)
FROM "Doctorfree"
WHERE (artist = "Yes" OR artist = "XTC") AND
      year < 1990
GROUP BY "**" + artist + "**"
```

- [Index of the Media Vault](../Media_Index.md)
- [README](../README.md)
- [Process](../Process.md)
