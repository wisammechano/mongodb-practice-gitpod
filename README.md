# MongoDB Queries Practice
The objectives of this assignment are:
1. Practicing MongoDB queries on a local database
2. Learning to query MongoDB collections directly before implementing the same in CRUD APIs

## Setup
Unlike the SQL assignment, this time we'll be working with a local database. So we will need to complete the local setup before we begin.

### Install MongoDB
Let's start by installing MongoDB on our local environments. Follow [these instructions on the MongoDB documentation](https://docs.mongodb.com/manual/installation/) to download and install MongoDB as per your OS.

You can also [follow these instructions from the Microsoft documentation](https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-database) if you are using WSL on your machine.

**NOTE** : Make sure to install the *Community Edition of MongoDB* and check that the version being installed is MongoDB 5.0, which is the latest release.

### Verify your installation
After following the installation instructions, run the following command:
```
mongod --version
```
You should see an output similar to this:
```
db version v5.0.3
Build Info: {
    "version": "5.0.3",
    "gitVersion": "657fea5a61a74d7a79df7aff8e4bcf0bc742b748",
    "modules": [],
    "allocator": "system",
    "environment": {
        "distarch": "x86_64",
        "target_arch": "x86_64"
    }
}
```
This confirms that we have installed MongoDB version 5.0.

### Run MongoDB
For Linux, run the command to start running the MongoDB service:
```
sudo systemctl start mongod
```
Verify that MongoDB has started successfully by running the command:
```
sudo systemctl status mongod
```

For MacOS, run the command to start running the MongoDB service:
```
brew services start mongodb-community@5.0
```
Verify that MongoDB has started successfully by running the command:
```
brew services list
```

### Prepare local database
To begin using MongoDB, connect the Mongo shell to the running instance simply by running the command: `mongosh`
It should show connection information and open a prompt looking like: `test>`

By default the local MongoDB setup includes a database called `test`. You can verify this now by running the command `db` and it should print the name of the current database which is `test`.

Let's create a new database called `practice`. Run this command: `use practice`. You should get an output `switched to db practice` and the prompt should change to `practice>`. This means we are now ready to use our new database.

If we now run the command `show collections` we can see that there are currently no collections on our database. On this assignment repo, you will find a file called `restaurants.json` which is a collection of restaurant data. Let's load this collection into our database. Open a new terminal window and run this command:
```
mongoimport --db practice --collection restaurants --drop --file /Path/to/your/file/restaurants.json
```
The output should mention:
```
3772 document(s) imported successfully
```

Now if we return to the terminal window running Mongo shell and run `show collections` again we will see that our database now has a collection called `restaurants`.

Let's run a query to look at the first document in the collection:
```
db.restaurants.findOne()
```

If you see all the details of the first restaurant, you have completed the setup successfully!

Looking at this first document, you should be able to understand the document model.
```
{
  _id: ObjectId,
  address: Object {
    building: String,
    coord: Array of numbers,
    street: String,
    zipcode: String
  },
  borough: String,
  cuisine: String,
  grades: Array of objects {date: Date, grade: String, score: Number},
  name: String,
  restaurant_id: String
}
```

If you want to exit the Mongo shell, you can just type the command: `exit`

## Practice Time
Let's perform some queries on our restaurants collection now. In this assignment repo, you will find another markdown file called `QUERIES.md`. In this file, we have listed many practice queries for you. Go through the questions one by one and try to execute the queries on your Mongo shell.

You can keep the MongoDB documentation open on your browser to help you with the queries.

As you finish executing your queries, paste the solutions in the provided space inside markdown code blocks syntax below each query statement.

## Submission
Once you're ready to submit the assignment, follow these steps on your terminal:
1. Stage your changes to the `QUERIES.md` file to be committed: `git add QUERIES.md`
2. Commit your final changes: `git commit -m "solve assignment"`
3. Push your commit to the main branch of your assignment repo: `git push origin main`

After your changes are pushed, return to this assignment on Canvas for the final step of submission.

## Conclusion
Now that we have practiced performing queries on a MongoDB database, we are ready for module 3 where we will learn to build a CRUD API using Express.js and a MongoDB ODM.