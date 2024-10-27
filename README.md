# Inlämningsrapport

## Skapa databas och samling

```javascript
use recipeDB
db.createCollection("recipes")
```

## Implementera grundläggande funktioner (CRUD) i mongshell

**1. Lägg till ett nytt recept (name, cookingTime, ingredients, steps)**

```javascript
db.recipes.insertOne({
  name: "Pancakes",
  cookingTime: 20,
  ingredients: ["flour", "milk", "eggs", "sugar", "butter"],
  steps: ["Mix ingredients", "Pour batter onto skillet", "Cook until golden on each side"]
})
```

**2. Visa alla recept**

```javascript
db.recipes.find()
```

**3. Uppdatera information för ett specifikt recept**

```javascript

db.recipes.updateOne(
  { name: "Pancakes" },
  { $set: { cookingTime: 25 } }
)

```

**4. Ta bort ett recept**

```javascript
db.recipes.deleteOne({ name: "Pancakes" })

```

## Implementera följande funktioner för en samling recept:

**1. Lägg till exakt 3 recept**

```javascript
db.recipes.insertMany([
  {
    name: "Spaghetti Bolognese",
    cookingTime: 30,
    ingredients: ["spaghetti", "minced meat", "tomato sauce", "onion", "garlic"],
    steps: ["Cook spaghetti", "Prepare sauce", "Mix and serve"]
  },
  {
    name: "Salad",
    cookingTime: 15,
    ingredients: ["lettuce", "tomato", "cucumber", "olive oil", "feta cheese"],
    steps: ["Chop vegetables", "Mix ingredients", "Add dressing"]
  },
  {
    name: "Grilled Chicken",
    cookingTime: 30,
    ingredients: ["chicken breast", "olive oil", "spices"],
    steps: ["Season chicken", "Grill chicken", "Serve"]
  }
])

```

**2. Visa alla recept**

```javascript
db.recipes.aggregate([
    { $sort: { cookingTime: 1 } }  
])
```

**3. Uppdatera information för många recept**

```javascript
// Uppdatera alla recept och lägg till ny rad i ingredienser 
db.recipes.updateMany(
    { ingredients: { $ne: "chili" } },  // Endast om det inte redan finns
    { $push: { ingredients: "chili" } }
)
```

**4. Ta bort många recept**

- Ta bort alla dokument i samlingen `recipes`

```javascript
db.recipes.deleteMany({})

db.recipes.deleteMany({ 
    $or: [
        { name: { $exists: true } },  // Om fältet namn existerar oavsett värde (inclusive tom sträng och null)
        { name: { $exists: false } }  // Fältet namn inte existerar 
    ]
})

db.recipes.find({name:'Grilled Chicken'}, {cookingTime: true }).limit(2)
```

- Ta bort de recept som matchar

```javascript
// Ta bort de recept vars tillagningstid överstiger 12 minuter
db.recipes.deleteMany({ cookingTime: { $gt: 12 } })
```

```javascript
// Ta bort de dokument där fältet namn är en tom sträng eller null
db.recipes.deleteMany({ $or: [{ name: "" }, { name: null }] })
```
**5. För att öka kvaliten på en Collection kan man använda sig av ett så kallat JSON-schema som säkerställer att du fyller i alla fält som är required och med rätt typ av data**

```javascript
{
  "$jsonSchema": {
    "bsonType": "object",
    "required": ["name", "cookingTime", "ingredients", "steps"],
    "properties": {
      "name": {
        "bsonType": "string",
        "description": "namnet på receptet, måste vara en sträng"
      },
      "cookingTime": {
        "bsonType": "int",
        "minimum": 1,
        "description": "tillagningstid i minuter, måste vara ett positivt heltal"
      },
      "ingredients": {
        "bsonType": "array",
        "items": {
          "bsonType": "string",
          "description": "varje ingrediens måste vara en sträng"
        },
        "description": "en lista av ingredienser, varje ingrediens är en sträng"
      },
      "steps": {
        "bsonType": "array",
        "items": {
          "bsonType": "string",
          "description": "varje steg måste vara en sträng"
        },
        "description": "en lista av tillagningssteg, varje steg är en sträng"
      },
      "difficulty": {
        "bsonType": "string",
        "enum": ["easy", "medium", "hard"],
        "description": "valfritt fält som anger svårighetsgraden på receptet"
      },
      "servings": {
        "bsonType": "int",
        "minimum": 1,
        "description": "valfritt fält som anger antal portioner, måste vara ett positivt heltal"
      }
    }
  }
}

```
**5.Exempel på denna collection **

```js
db.createCollection("recipes", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "cookingTime", "ingredients", "steps"],
      properties: {
        name: { bsonType: "string" },
        cookingTime: { bsonType: "int", minimum: 1 },
        ingredients: {
          bsonType: "array",
          items: { bsonType: "string" }
        },
        steps: {
          bsonType: "array",
          items: { bsonType: "string" }
        },
        difficulty: {
          bsonType: "string",
          enum: ["easy", "medium", "hard"]
        },
        servings: { bsonType: "int", minimum: 1 }
      }
    }
  }
})

```

