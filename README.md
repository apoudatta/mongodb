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
    # get 20 data
    db.books.find()
    db.books.find({author: "Terry"})
    db.books.find({author: "Nasim Uddin", rating: 7})
```

Take only title and author

```bash
    db.books.find({author: "Nasim Uddin", rating: 7}, {title: 1, author: 1})
    db.books.find({}, {title: 1, author: 1})
```

#### Find single item

```bash
    db.books.findOne({_id: ObjectId('6704e3a99cd6771c3bc73bf8')})
```

#### Count, Limit, Sorting(1:asc, -1:desc)

```bash
    db.books.find().count()
    db.books.find({ author: "Nasim Uddin" }).count()
    db.books.find().limit(3)
    db.books.find().sort({ title: 1 })
    db.books.find().sort({ title: -1 }).limit(3)
```

#### Nested Documents

```bash
    db.books.insertOne({ title: "The Way of Kings", author: "Brandon Sanderson", rating: 9, pages: 400, genres: ["fantasy"], reviews: [{name: "Yoshi", body: "Great book!"},{name: "mario", body: "so so"}] })
```

#### Operators & Complex Queries

```bash
    # get document greater then 7
    db.books.find({ rating: {$gt: 7}})
    # get document less then 7
    db.books.find({ rating: {$lt: 7}})
    # get document less then or equal to 7
    db.books.find({ rating: {$lte: 9}})
    # get document less then or equal to 7 and author "Brandon Sanderson"
    db.books.find({ rating: {$lte: 9}, author: "Brandon Sanderson"})
    # or
    db.books.find({$or: [{ rating: 7}, {author: "Brandon Sanderson"}]})
    # pages less then 300 or greater then 400
    db.books.find({$or: [{ pages: {$lt: 300}}, { pages: {$gt: 400}}]})
    # in
    db.books.find({rating: {$in: [7,8,9]}})
    # not in
    db.books.find({rating: {$nin: [7,8,9]}})
```

#### Querying Arrays

```bash
    # take where one array element fantasy
    db.books.find({genres: ["fantasy"]})
    # take all element where include fantasy
    db.books.find({genres: {$all: ["fantasy"]}})
    # find review array name value
    db.books.find({"reviews.name": "Yoshi"})
```

#### Deleting Documents

```bash
    db.books.deleteOne({_id: ObjectId('6704cf509a55e91a77d6e825')})
    db.books.deleteMany({author: 'Nasim Uddin'})
```

#### Updating Documents

```bash
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf8')}, {$set: {rating: 3, pages: 30}})
    db.books.updateMany({author: 'Nasim Uddin'}, {$set: { author: 'Nasim' }})
    # Increment value
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf8')}, {$inc: {pages: 2}})
    # Decrement value
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf8')}, {$inc: {pages: -2}})
    # pull or remove a value array item
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf9')}, {$pull: {genres: "dystopian"}})
    # Push or add a value array item
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf9')}, {$push: {genres: "dystopian push"}})
    #Push or add multiple item into array
    db.books.updateOne({_id: ObjectId('6704ece8d8e2545dd8c73bf9')}, {$push: {genres: {$each: ["1","2"]}}})
```

#### Drivers

```bash
    # Initialize npm
    npm init
    # install Express
    npm install express --save
    # install nodemon
    npm install -g nodemon
    # install mongodb driver
    npm install mongodb@6.9
    # run nodemon
    nodemon app
```

### APIs

Get all item
GET http://localhost:3000/books?page=2

Insert item
POST http://localhost:3000/books

```bash
    {
        "title": "The Final Empire",
        "author": "Brandon Sanderson",
        "rating": 9,
        "pages": 420,
        "genres": [
            "fantasy",
            "magic"
        ],
        "reviews": [
            {
                "name": "Shaun",
                "body": "Coudn't put this book down."
            },{
                "name": "Chun-Li",
                "body": "Love it."
            }
        ]
    }
```
