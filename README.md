# Inlämningsrapport

## Skapa databas och samling

```javascript
use recipeDB
db.createCollection("recipes")
```

## Implementera grundläggande funktioner (CRUD) i `mongosh`

**1. Lägg till ett nytt recept (namn, ingredienser, tillagningssteg, tillagningstid)**

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
    { ingredients: { $ne: "salt och peppar efter smak" } },  // Endast om det inte redan finns
    { $push: { ingredients: "salt och peppar efter smak" } }
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
// Ta bort de recept vars tillagningstid överstiger 60 minuter
db.recipes.deleteMany({ cookingTime: { $gt: 12 } })
```

```javascript
// Ta bort de dokument där fältet namn är en tom sträng eller null
db.recipes.deleteMany({ $or: [{ namn: "" }, { namn: null }] })
```
