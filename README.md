# Role-Based Access Control (Admin/User/Moderator)
Build role-based access control with Admin, User, and Moderator roles using Node.js and Express.js
## Objective
Learn how to implement role-based access control (RBAC) in a Node.js and Express application to restrict access to certain routes or actions based on user roles. This task helps you understand how to store and check user roles in JWT tokens, create flexible authorization logic, and secure sensitive parts of your backend API.
## Task Description
Create a Node.js and Express.js backend that supports user authentication with different roles, including Admin, User, and Moderator. Implement a login route that issues JWT tokens containing the user's role in the payload. Create middleware to verify the JWT and extract the user's role. Implement separate protected routes that can only be accessed by specific roles, for example:
- An **Admin-only dashboard route**
- A **Moderator management route**
- A general **User profile route**
Ensure that requests with invalid tokens or insufficient roles are properly denied with clear error messages. Test your system by logging in with different roles and accessing each route to confirm that the role-based restrictions work as expected.
## Documentation Images
![Image 1](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/7.png)
![Image 2](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/8.png)
![Image 3](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/9.png)
![Image 4](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qnt88p4/10.png)

---

# E-commerce Catalog with Nested Document Structure in MongoDB

## Objective
Learn how to design and implement a MongoDB data model using nested documents to represent a real-world e-commerce catalog. This task strengthens your understanding of MongoDB's flexible document structure, schema design, and handling complex relationships inside a single collection.

## Task Description
Create a MongoDB collection to represent an e-commerce catalog. Each product document should include fields such as name, price, category, and an array of nested variants. Each variant should include details like color, size, and stock. Insert a few sample product documents demonstrating different variants. Then, implement queries to retrieve all products, filter products by category, and project specific variant details. Use MongoDB shell queries or Mongoose methods to show how nested documents can be accessed and manipulated effectively.

## Implementation

### 1. Creating the Collection and Inserting Sample Documents

```javascript
// MongoDB Shell - Create and Insert Sample Products
db.products.insertMany([
  {
    name: "Classic T-Shirt",
    price: 29.99,
    category: "Clothing",
    variants: [
      { color: "Red", size: "M", stock: 50 },
      { color: "Red", size: "L", stock: 30 },
      { color: "Blue", size: "M", stock: 45 },
      { color: "Blue", size: "L", stock: 25 }
    ]
  },
  {
    name: "Denim Jeans",
    price: 59.99,
    category: "Clothing",
    variants: [
      { color: "Black", size: "32", stock: 20 },
      { color: "Black", size: "34", stock: 15 },
      { color: "Blue", size: "32", stock: 30 },
      { color: "Blue", size: "34", stock: 22 }
    ]
  },
  {
    name: "Wireless Headphones",
    price: 89.99,
    category: "Electronics",
    variants: [
      { color: "Black", size: "Standard", stock: 100 },
      { color: "White", size: "Standard", stock: 80 },
      { color: "Silver", size: "Standard", stock: 60 }
    ]
  },
  {
    name: "Running Shoes",
    price: 79.99,
    category: "Footwear",
    variants: [
      { color: "Black", size: "9", stock: 25 },
      { color: "Black", size: "10", stock: 30 },
      { color: "White", size: "9", stock: 20 },
      { color: "White", size: "10", stock: 35 }
    ]
  }
]);
```

### 2. Query to Retrieve All Products

```javascript
// MongoDB Shell - Retrieve all products
db.products.find().pretty();

// Or with Mongoose
const products = await Product.find();
console.log(products);
```

### 3. Query to Filter Products by Category

```javascript
// MongoDB Shell - Filter by category
db.products.find({ category: "Clothing" }).pretty();

// Get all Electronics
db.products.find({ category: "Electronics" }).pretty();

// With Mongoose
const clothingProducts = await Product.find({ category: "Clothing" });
console.log(clothingProducts);
```

### 4. Query to Project Specific Variant Details

```javascript
// MongoDB Shell - Project only product name and variants with specific color
db.products.find(
  { "variants.color": "Black" },
  { name: 1, price: 1, "variants.$": 1 }
).pretty();

// Find products with variants in stock greater than 30
db.products.find(
  { "variants.stock": { $gt: 30 } },
  { name: 1, category: 1, variants: 1 }
).pretty();

// Project specific fields and filter variants
db.products.aggregate([
  { $match: { category: "Clothing" } },
  { $unwind: "$variants" },
  { $match: { "variants.stock": { $gte: 20 } } },
  { $project: {
      name: 1,
      price: 1,
      "variant.color": "$variants.color",
      "variant.size": "$variants.size",
      "variant.stock": "$variants.stock"
    }
  }
]);

// With Mongoose - Find and project specific variant details
const productsWithBlackVariants = await Product.find(
  { "variants.color": "Black" },
  { name: 1, price: 1, variants: { $elemMatch: { color: "Black" } } }
);
console.log(productsWithBlackVariants);
```

### 5. Advanced Queries - Updating Nested Documents

```javascript
// MongoDB Shell - Update stock for a specific variant
db.products.updateOne(
  { name: "Classic T-Shirt", "variants.color": "Red", "variants.size": "M" },
  { $set: { "variants.$.stock": 60 } }
);

// Add a new variant to an existing product
db.products.updateOne(
  { name: "Running Shoes" },
  { $push: { variants: { color: "Red", size: "11", stock: 40 } } }
);

// With Mongoose
await Product.updateOne(
  { name: "Wireless Headphones", "variants.color": "Black" },
  { $inc: { "variants.$.stock": -5 } }
);
```

## Expected Output

![MongoDB Collection Example](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qdbdjd4/7.png)

![Query Results](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qdbdjd4/8.png)

![Variant Projection](https://s3.ap-south-1.amazonaws.com/static.bytexl.app/uploads/42vxd5kz7/content/43qdbdjd4/111111.png)

## Key Concepts

- **Nested Documents**: Variants are embedded within product documents, demonstrating MongoDB's flexible schema
- **Array Operations**: Querying and manipulating arrays of nested documents
- **Projection**: Selecting specific fields and array elements to return
- **Aggregation Pipeline**: Using `$unwind`, `$match`, and `$project` for complex queries
- **Update Operations**: Modifying nested documents using positional operators
