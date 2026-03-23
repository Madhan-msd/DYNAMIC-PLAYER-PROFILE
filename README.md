# 🏏 Dynamic Player Profile – MongoDB Project

This project demonstrates a Dynamic Player Profile system using MongoDB. It stores player details and performs various database operations dynamically.

## Database
use playerDB

## Collection
db.createCollection("players")

## Insert Operation
db.players.insertMany([
  { name: "Virat Kohli", age: 35, team: "India", role: "Batsman", runs: 12000 },
  { name: "Rohit Sharma", age: 36, team: "India", role: "Batsman", runs: 10000 },
  { name: "MS Dhoni", age: 42, team: "India", role: "Wicket Keeper", runs: 9000 },
  { name: "Joe Root", age: 33, team: "England", role: "Batsman", runs: 11000 },
  { name: "Steve Smith", age: 34, team: "Australia", role: "Batsman", runs: 9500 }
])
Output: (See screenshot)

## Read Operations

### Find All
db.players.find().pretty()
Output: (See screenshot)

### Find One
db.players.findOne({ name: "Virat Kohli" })
Output: (See screenshot)

### Filter (Team India)
db.players.find({ team: "India" })
Output: (See screenshot)

### Condition (Runs > 10000)
db.players.find({ runs: { $gt: 10000 } })
Output: (See screenshot)

## Projection
db.players.find({}, { name: 1, team: 1, _id: 0 })
Output: (See screenshot)

## Update
db.players.updateOne(
  { name: "Virat Kohli" },
  { $set: { runs: 12500 } }
)
Output: (See screenshot)

## Delete
db.players.deleteOne({ name: "MS Dhoni" })
Output: (See screenshot)

## View
db.createView("indiaPlayers", "players", [
  { $match: { team: "India" } }
])
Output: (See screenshot)

## Validation
db.createCollection("players_validation", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "age", "team"],
      properties: {
        name: { bsonType: "string" },
        age: { bsonType: "int", minimum: 0 },
        team: { bsonType: "string" }
      }
    }
  }
})

## Validation Insert
db.players_validation.insertOne({
  name: "Virat Kohli",
  age: 35,
  team: "India"
})
Output: (See screenshot)

## Verify
db.players.find().pretty()
Output: (See screenshot)

## Screenshots
All outputs are available in the screenshots folder.

## Conclusion
This project demonstrates CRUD operations, filtering, projection, view creation, and validation using MongoDB for managing dynamic player profiles.
