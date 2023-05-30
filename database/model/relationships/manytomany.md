# ManyToMany

```dart
@DoxModel()
class Artist extends ArtistGenerator {
  ... 

  @ManyToMany(Song)
  List<Song> songs = [];
}

@DoxModel()
class Song extends SongGenerator {
  ... 

  @ManyToMany(Artist)
  List<Artist> artists = [];
}
```

```dart
class ManyToMany {
  final Type model;
  final Function? onQuery;
  final bool? eager;

  /// id column on artist table
  final String? localKey;

  /// id column on song table
  final String? relatedKey;

  /// artist_id column on related table
  final String? pivotForeignKey;

  /// artist_id column on related table
  final String? pivotRelatedForeignKey;

  /// artist_song table
  final String? pivotTable;

  const ManyToMany(
    this.model, {
    this.eager,
    this.onQuery,
    this.localKey,
    this.relatedKey,
    this.pivotForeignKey,
    this.pivotRelatedForeignKey,
    this.pivotTable,
  });
}

```

{% hint style="warning" %}
As a default, pivot table will be named alphabetically. \
\
Eg. if we have \
**1** .**`song`** and **`artist`** table => **`artist_song`**\
**`2`**.**`blog`** and **`category`** table => **`blog_category`**\
\
But you still can give custom name to **`pivotTable`** param\

{% endhint %}
