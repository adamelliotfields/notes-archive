# Morphia Notes
> :calendar: *August 30, 2017*

### Connecting to MongoDB

```java
final Morphia morphia = new Morphia();

// The location of classes to be mapped
// mapPackage can be called on multiple packages
morphia.mapPackage("io.github.adamelliotfields");

// Passing no arguments to the MongoClient constructor will assume the default host and port
// mongodb://localhost:27017
final Datastore datastore = morphia.createDatastore(new MongoClient(), "database_name");
```

When testing, you can call `datastore.getDB().dropDatabase()` to drop the database.

### Mapping Classes
Classes can be top level entities (documents) or embedded in other documents (subdocuments).

Note that classes must have a no-argument constructor (which can be private) to be used by Morphia.

```java
@Entity("posts")   // morphia
@Data              // lombok
@NoArgsConstructor // lombok
class Post {
  @Id
  private ObjectId id;
  
  private String title;
  private String content;
  private LocalDate date;

  public Post(String title, String content) {
    this.title = title;
    this.content = content;
    this.date = LocalDate.now();
  }
}
```

### Adding Documents

```java
final Post newPost = new Post("Title", "Some text.");

datastore.save(newPost);
```

### Querying Collections

```java
// Return a list of all posts
final Query<Post> query = datastore.createQuery(Post.class);
final List<Post> posts = query.asList();

// Shorthand
final List<Post> posts = datastore
                           .find(Post.class)
                           .asList();

// Get the first entity in the results set
final Post post = datastore
                    .find(Post.class)
                    .get();

// Filter the results
final Post post = datastore
                    .find(Post.class)
                    .filter("title", "Title")
                    .get();

// Alternatively
final Post post = datastore
                    .find(Post.class)
                    .field("title")
                    .equalIgnoreCase("Title")
                    .get();
```

### Updating Documents

```java
final Query<Post> query = datastore
                            .createQuery(Post.class)
                            .filter("id", id);

final UpdateOperations<Post> update = datastore
                                        .createUpdateOperations(Post.class)
                                        .set("title", "New Title");

// datastore.update() returns an object with details of the update operation
final UpdateResults updateResults = datastore.update(query, update);

// UpdateResults {
//   wr=WriteResult {
//     n=1,
//     updateOfExisting=true,
//     upsertedId=null
//   }
// }
```

### Deleting Documents

```java
final Query<Post> query = datastore
                            .createQuery(Post.class)
                            .filter("title", "New Title");

datastore.delete(query);
```

### [Annotations](http://mongodb.github.io/morphia/1.3/guides/annotations/)
 - `@Entity` - Takes a string that names the collection for the entity to be saved in
 - `@Id` - Marks a field to be the `_id` field in MongoDB
 - `@Property` - Takes a string to be used as the property name in MongoDB (optional)
 - `@Validation` - Takes a string validation schema to be applied
 - `@Embedded` - Embeds the document as a subdocument
 - `@Reference` - Marks a field as a reference to another document

### [Lifecycle Annotations](http://mongodb.github.io/morphia/1.3/guides/lifeCycleMethods/)
 - `@PreLoad` - Called before mapping the datastore object to the entity (POJO)
 - `@PostLoad` - Called after mapping to the entity
 - `@PrePersist` - Called before save; can return a `DBObject` in place of an empty one
 - `@PreSave` - Called before the save call to the datastore
 - `@PostPersist` - Called after the save call to the datastore

### [Indexing Annotations](http://mongodb.github.io/morphia/1.3/guides/indexing/)
 - `@Indexes` - Defines a list of indices
 - `@Index` - Defines an index
 - `@IndexOptions` - Defines the options to be used when declaring an index
 - `@Field` - Defines a field to be used in an index

```java
@Entity
@Indexes({
  @Index(fields = @Field("field2", type = DESC)),
  @Index(fields = @Field("field3", options = @IndexOptions(name = "indexing_test")))
})
public class IndexExample {
  @Id
  private ObjectId id;
  private String field;
  @Property
  private String field2;
  @Property("f3")
  private String field3;
}
```

### `filter`
The `Query` instance method `filter` takes two arguments: a condition string and a value.

At its simplest, the condition is just a field name. The condition can also be an operator.

The list of operators can be found in the [`FilterOperator`](http://mongodb.github.io/morphia/1.3/javadoc/org/mongodb/morphia/query/FilterOperator.html)
enum.

### `field`
The `Query` instance method `field` takes only one argument - a field name string - and returns a
`FieldEnd` object.

The list of operation methods can be found in the [`FieldEnd`](http://mongodb.github.io/morphia/1.3/javadoc/org/mongodb/morphia/query/FieldEnd.html)
interface.
