# mongodb

## command

#### Connect mongo server

```bash
    mongosh
```

#### Show all DB

```bash
    show dbs
```

#### Use a DB

```bash
    use bookstore
```

#### show all collections/table

```bash
    show collections
```

#### Go to a collections

```bash
    db.books
```

#### Insert one

```bash
    db.books.insertOne(
        {
            title: "The color of magic",
            author: "Terry Pratchett",
            pages: 300,
            rating: 7,
            genres: ["fantasy", "magic"]
        }
    )
```

#### Insert new collections

```bash
db.authors.insertOne({ name: "Brandon Sanderson", age: 60 })
```

#### Insert multiple data

```bash
db.books.insertMany([{title: "The Light", author: "Terry", pages: 250, rating: 6, genres:["fantasy"]},{title: "Dune", author: "Frank", pages: 500, rating: 10, genres:["sci-fi", "dystopian"]}])
```

#### Find data from a collection

```bash
 db.books.find({author: "Terry"})
```
