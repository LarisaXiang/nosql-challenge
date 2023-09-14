# nosql-challenge

Part 2: Update the Database
# Change the `RatingValue` to integers
$toInt will throw an error if it encounters a value that cannot be converted to an integer. The $convert operator with the onError option provides a way to handle such conversion errors gracefully by setting a default value (like 0 in the example you provided). If use $toInt, need to ensure beforehand that all RatingValue fields either contain values that can be safely converted to integers or handle potential exceptions in your application code.

Part 3: Exploratory Analysis
# cursor vs query 
Definition: A cursor is a database object used to traverse the results of a query. When you execute a query that retrieves multiple records, instead of getting all records at once, you get a cursor. This cursor points to a specific location within the result set and can be used to fetch records one-by-one or in batches.
Usage: In many programming environments that interface with databases, the result of a SELECT query or its equivalent is often a cursor. For example, in MongoDB's Python driver (PyMongo), when you execute a find() method, you get a cursor object.
Purpose: Cursors allow for efficient retrieval and traversal of query results, especially when the result set is large. Instead of loading all results into memory, cursors allow you to fetch records as you need them.

Definition: A query is a request for data or information from a database table or combination of tables. It is an expression that specifies what data you want to retrieve, update, delete, or manipulate.
Usage: In SQL databases, a query is usually written in SQL (Structured Query Language). For example: SELECT * FROM users WHERE age > 30;. In NoSQL databases like MongoDB, queries are typically expressed as JSON-like structures.
Purpose: A query defines a specific set of criteria to filter, transform, or aggregate data.

# hygiene20_df = pd.DataFrame(hygiene_20) vs hygiene20_df = pd.DataFrame(list(hygiene_20))
Both codes achieve the same result because they both convert a MongoDB cursor (result from a .find() operation) into a Pandas DataFrame. 
If directly passing the cursor hygiene_20 to the pd.DataFrame() constructor. The DataFrame constructor can take an iterable (like a list or a MongoDB cursor) and convert it into a DataFrame. Since the cursor is iterable, the DataFrame constructor will iterate over it and retrieve all the documents.
However, if first converting the cursor hygiene_20 into a list using the list() function. The resulting list is then passed to the pd.DataFrame() constructor. This method is a more explicit way of fetching all the results from the cursor and converting them into a list, which is then turned into a DataFrame.
Both methods are valid and will produce the same result. The first method is more concise, but the second method makes it clear that you're converting the cursor to a list before constructing the DataFrame.
it's important to remember that cursors in MongoDB are stateful. This means that once you've iterated over them, you can't iterate over them again from the beginning without re-querying. In such cases, the second approach (using list()) is beneficial because it makes it clear that you're consuming the cursor completely. If you try to use an already-consumed cursor in the first approach, you'll end up with an empty DataFrame.