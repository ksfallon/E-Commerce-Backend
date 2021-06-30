<h1 align ="center"> E-Commerce-Backend </h1>

Link to [First Half of VLC and Insominia Walkthru](https://youtu.be/jp6N06c48Mg).
<br>
Link to [Second Half of VLC and Insominia Walkthru](https://youtu.be/ElbogKglLSE).
<br>
Link to [Github page](https://github.com/ksfallon/E-Commerce-Backend).
### **TABLE OF CONTENTS:**
1. [Overview of E-Commerce-Backend](#1-overview-of-e-commerce-backend)
2. [Files & Modules needed to start](#2-files-and-modules-needed-to-start)
3. [Creating a Secure connection with **dotenv** and **sequelize**](#3-creating-a-secure-connection-with-dotenv-and-sequelize)
4. [Creating the *columns* inside **models**](#4-creating-the-columns-inside-models)
5. [Creating the **api routes**](#5-creating the-api-routes)
6. [Screen Shots of App with Inspect/Console](#6-screen-shots-of-app)
7. [License for Repository](#7-license)

<br>

## 1. Overview of E-Commerce Backend
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

## 4. Creating the **api routes**

## 5. The api routes js Files

## 6. 

## 7. License
Licensed under the [MIT License](https://choosealicense.com/licenses/mit/#).
