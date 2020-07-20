# GoFinances-backend
GoFinances, a transaction manager built with Node.js and TypeScript.

### Overview
GoFinances backend/server has 4 routes to manage the transactions.

**GET** on `/transactions` -> Returns an object with 2 objects inside, one with all transactions on the database and other with balance information (`income`, `outcome`, `total`).  
**POST** on `/transactions` -> Send a JSON body with `title`, `value`, `type`, `category`. `type` has to be either 'income' or 'outcome'. This request will create the transaction on the database and also create the category in case it doesn't exists yet, if it exists it will use the previously created category_id. Response returns an object with all the sent information, category details (`id`, `title`, `created_at`, `updated_at`), an `id` and both `created_at`/`updated_at`.  
**POST** on `/transactions/import` -> Send a CSV file with the transactions following this format [here](https://github.com/PooWoox/GoFinances-web/blob/master/src/utils/file.csv). It'll add the transactions to the database and return an array with an object with each transaction detail.  
**DELETE** on `/transactions/:id` -> Send the id of the transaction you want to delete. It returns a 204 status with no content.

### :computer: Local testing
To run this application on your machine you will need to have Docker and a database tool to visualize Postgres database (like DBeaver etc.). You can read how to set up a postgres image on your docker [here](https://hub.docker.com/_/postgres/) in case you don't have a connection set up. After setting it up and starting the container, connect to the database tool of your choice and create a database with the name of your choice (note that the name you choose will have to be updated on the `ormconfig.json` file that is on the root directory, just update everything you do differently).

After setting up the database, start by installing all the necessary dependencies for the project using `yarn` or `npm install` if you prefer npm (remember to delete the `yarn.lock` file in case you decide to use npm).

Then run all migrations using the command `typeorm migration:run`. After running the migrations all tables should appear on your database if everything was configured correctly.

Finally, run `yarn dev:server` or `npm dev:server` on your terminal to start the application on port 3333. Test the routes to see if everything is working correctly.
