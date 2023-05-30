# Relationships

### HasOne

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

<strong>  @HasOne(BlogInfo)
</strong>  BlogInfo? blogInfo;
}
</code></pre>

### HasMany

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

<strong>  @HasMany(Comment)
</strong>  List&#x3C;Comment> comments = [];
}
</code></pre>

### BelongsTo

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Comment extends CommentGenerator {
  ... 

<strong>  @BelongsTo(Blog)
</strong>  Blog? blog;
}
</code></pre>

### ManyToMany

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Artist extends ArtistGenerator {
  ... 

<strong>  @ManyToMany(Song)
</strong>  List&#x3C;Song> songs = [];
}

@DoxModel()
class Song extends SongGenerator {
  ... 

<strong>  @ManyToMany(Artist)
</strong>  List&#x3C;Artist> artists = [];
}
</code></pre>

### Eager Loading

#### `eager: true`

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

<strong>  @HasOne(BlogInfo, eager: true)
</strong>  BlogInfo? blogInfo;
}
</code></pre>

#### `$getRelation('relation_name')`

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

  @HasOne(BlogInfo)
  BlogInfo? blogInfo;
}

Blog blog = Blog().find(1);
<strong>await blog.$getRelation('blogInfo');
</strong>
print(blog.blogInfo);
</code></pre>

#### `preload('relation_name')`

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

  @HasOne(BlogInfo)
  BlogInfo? blogInfo;
}

<strong>Blog blog = Blog().preload('blogInfo').find(1);
</strong>
print(blog.blogInfo);
</code></pre>

#### `related('relation_name')`

<pre class="language-dart"><code class="lang-dart">@DoxModel()
class Blog extends BlogGenerator {
  ...

  @HasOne(BlogInfo)
  BlogInfo? blogInfo;
}

Blog blog = Blog().find(1);
BlogInfo? bloginfo = blog
<strong>  .related('blogInfo')?
</strong>  .where('id', 2)
  .getFirst()

print(bloginfo);
</code></pre>
