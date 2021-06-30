<h1 align ="center"> E-Commerce-Backend </h1>

Link to [First Half of VLC and Insominia Walkthru](https://youtu.be/jp6N06c48Mg).
<br>
Link to [Second Half of VLC and Insominia Walkthru](https://youtu.be/ElbogKglLSE).
<br>
Link to [Github page](https://github.com/ksfallon/E-Commerce-Backend).
### **TABLE OF CONTENTS:**
1. [Overview of E-Commerce-Backend](#1-overview-of-ecommerce-backend)
2. [Files & Modules needed to start](#2-files-and-modules-needed-to-start)
3. [Creating a Secure connection with **dotenv** and **sequelize**](#3-creating-a-secure-connection-with-dotenv-and-sequelize)

4. [Creating the *columns* inside **models**](#4-creating-the-columns-inside-models)
5. [Creating the **api routes**](#5-creating-the-api-routes)
6. [Screen Shots of App with Inspect/Console](#6-screen-shots-of-app)
7. [License for Repository](#7-license)

<br>

## 1. Overview of ECommerce Backend
- For this project I used [mysql2](https://www.npmjs.com/package/mysql2) and [sequelize](https://www.npmjs.com/package/sequelize) to connect MySQL Database to my VSCode. [dotenv](https://www.npmjs.com/package/dotenv) is used to store sensitive data, such as my MySQL password, username and the name of the database used. In the model's, each table is given a column that contains its keys and in the model/index.js column definitions are used to connect the tables through understood foreign keys.
<br>

## 2. Files and Modules needed to start
 **Modules imported:**
 - [express](https://www.npmjs.com/package/express)
 - [mysql2](https://www.npmjs.com/package/mysql2)
 - [dotenv](https://www.npmjs.com/package/dotenv)
 - [sequelize](https://www.npmjs.com/package/sequelize)
 
 **Files that needed to be Modified**
 - **.env.EXAMPLE** and **server.js** to create our secure connection.
 - All Files inside **models** folder
 - Three files inside **routes/api** folders: **product-routes.js**, **category-routes.js** and **tag-routes.js**

## 3. Creating a Secure Connection with **dotenv** and **sequelize**
1. To get the connection running I needed to edit and update my .env.EXAMPLE file:
 - I first needed to change the name to ".env" so the connection.js could recognize it.
 - Then I needed to add the name I created for my database: DB_NAME = ? to *ecommerce_db* , the DB_USER = ? to *'root'* and then add my personal password in the DB_PW.
 - <br>
2. Because **dotenv** is already required in my connection.js file and plus *sequelize* the code will provide the second part to our secure connection. The sequelize code provides a place for the dotenv code to be placed.
`new Sequelize(process.env.DB_NAME, process.env.DB_USER, process.env.DB_PW`
 - *this is only a portion of the code

3. Finally in **server.js** you have to import **sequelize** so I required it.
 - *This is important not only for the secure connection but is also very important for allowing MySQL to connect to my repository.


## 4. Creating the *columns* inside **models** 
1. I needed to create columns for the models: **Category.js**, **Product.js**, **ProductTag.js** and **Tag.js**
- All of them have const of Model and DataTypes that require **sequelize** 
    - Each is a class that extends Model.js
- All have a const sequelize and require the connection.js file.
    - At the end of each column is the *sequelize* object that extends *Model*, sets specific parameters for the model, such as "underscored: true" that sets all camel cases to underscored. 
    - And it sets the "modelname" for each model - 'category', 'tag', 'product' and 'productTag'
- And finally all of them end with "module.exports" and the class is exported there. Ex: `module.exports = Tag;`
<br>
2. **Category.js** 
- *Category* has two keys, an *id* and *category_name*. For *id* there are four requirements - which are the same for all models. 
    `    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },`
    - The data type of the id is an integer. 
    - It cannot be allowNull
    - It is Category's primaryKey
    - it auto increments so there is never an overlap in id numbers. 
    - *The primaryKey is what is used to associate the tables in the index. The primary key of category is used as a foreign key in product as category_id
- *category_name* only has two requirements - the data type is a string and it cannot be null.
<br>
3. **Tag.js**
- it has two keys *id* and *tag_name*.
- **id** : same requirements as *category.id*
- - **tag_name** : same requirements as *category.category_name*
<br>
4. **Product.js**
- Product has the most keys -5: *id*, *product_name*, *price*, *stock* and *category_id*
- **id** : same requirements as *category.id*
- **product_name** : same requirements as *category.category_name*
- **price** : It is a decimal datatype and i call 10 for the left side of the decimal and 2 for the right side so the max number of values on each side. It cannot be null and it is a decimal.
- **stock** : its an integer data typem it cannot be null, if no value is entered than the default is 10, and it is a number.
- **category_id** : is an integer and most importantly it is the foreign key that associates product with category.
    - It references the model 'category' on the key 'id'.
    - **Because of this reference we DO NOT have to call a foreign key in the associations made in our *model/index.js* file**.
<br>
5. **ProductTag.js**
- *ProductTag* has 3 keys: *id*, *product_id* and *tag_id*.
- **id** : same requirements as *category.id*
- **product_id** : is an integer and most importantly it is the foreign key that associates *ProductTag* with *Product*.
    - It references the model 'product' on the key 'id'.
- **tag_id** : is an integer and most importantly it is the foreign key that associates *ProductTag* with *Tag*.
    - It references the model 'product' on the key 'id'.
- **Because of these references we DO NOT have to call a foreign key in the associations made in our *model/index.js* file**.
<br>
6. Last I needed to make the associations between the models in the **models/index.js**
- All of the models are already required as constants at the top of **index.js** page.
- In each association i have to explain how these tables are connected to one another.
    - `Product.belongsTo(Category,{})`
        - Product is the child table to Category, and cannot be made until the category table is made. - The FK is called in the models. and by saying 'one-thing' belongs to 'another-thing', automatically adds 'another-thing'ID to 'one-things' table. 
    - `Category.hasMany(Product,{})`
        - Category is the parent table to Product. and hasMany creates that association.
    - `Product.belongsToMany(Tag, {through: {model: ProductTag, unique: false},})`
    and
    `Tag.belongsToMany(Product, {through: {model: ProductTag, unique: false},})`
        - Products and Tags belong to each other though the *ProductTag* table, which has product_id and tag_id as FK to that connect to Product by product.id and Tag by tag.id

## 4. Creating the **api routes**
Under the routes folder is the index.js and the api folder. This index.js requires express and api routes and creates that intial route and connection.
- Within the api folder is another index.js. This one requires express and all the api route files (categoryRoutes, productRoutes and tagRoutes). It creates the routes for each of these files with *router.use* and gives each one its own extension suchs as '/categories'.
- For each route I needed to create:    
    - GET for ALL and for ID
    - POST to create a new object 
    - PUT to update an exsisting object
    - DELETE to delete an exsisting object
- the GET, POST and PUT and DELETE methods are all basically the same for each route. so I will just explain **category-routes.js**
1. GET ALL
    - It is a promise so I include async (right before the req,res) and await right before "Category.findAll". to ensure that data is collected before the status 200 or the status 500 is given.
    - I'm using try catch as well. The try holds the const categoryData which equals the category.findAll function. 
        - Within that function I include model product so all products associated with each category is shown with that individual category in the array of all categories.
    - if the try is successful the result is a status of 200 and the categoryData (the json) is displayed.
    - If the try isn't successful there is a catch that catches this error, and the status 500 and error is displayed.
2. GET by ID 
    - This is the same layout as the GET ALL with a few little tweeks.
    - the router.get goes to localhost:3001/api/categories/:id, where as in GET ALL the "/:id" is not needed.
    - our function is "Category.findByPk" so we need to find by a specific primary key and to get that specific we need the req.paramas.id (the id typed into the '/:id' spot).
    - I still use async and away, try and catch in the same places and I still include model:Product.
3. POST to CREATE a new category.
    - Just like GET I'm using async and await in the same places for the promise as well as try and catch so an error will be produced if the newCategory isn't successfully created.
    - The new function is "Category.create" and it asks to create a newCategory by providing a value to the key *category_name* with the req.body.category_name provided. Do add these new items or categories it can be tested and is done in Insominia.
4. PUT to UPDATE an exsisting category
    - Just like GET I'm using async and await in the same places for the promise as well as try and catch so an error will be produced if the newCategory isn't successfully created.
    - The new function is "Category.update" and it asks to update with the request body (req.body) WHERE the updateCatData current req.body.id is. So the the ID that is requested is called and the information from that id i need to update is updated.
    - Do add these new items or categories it can be tested and is done in Insominia.
5. DELETE to DELETE an exsisting category
    - Just like GET I'm using async and await in the same places for the promise as well as try and catch so an error will be produced if the newCategory isn't successfully created.
    - Just like GET ID i need to include '/:id'
    - The new function is "Category.destroy" and it deletes WHERE the req.body.id is. So the the ID that is requested is called and it is then deleted.
    - Do add these new items or categories it can be tested and is done in Insominia.
6. In Product CREATE and PUT it is slightly more complicated because it is a bulkCreate to update all of the ProductTags And this was provided for us.
## 5. Using MySQL and Insominia 

## 6. License
Licensed under the [MIT License](https://choosealicense.com/licenses/mit/#).
