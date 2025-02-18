# Visitor Management System

This project is a Visitor Management System built using Node.js and PostgreSQL. It allows users to manage visitor data, including adding, updating, viewing, and deleting visitor records.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- [Node](https://nodejs.org/en/download/package-manager) (version 22.6.0 or later)
- [Docker](https://docs.docker.com/get-docker/) (version 20.10 or later)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.29 or later)
- [Git](https://git-scm.com/downloads)

## Getting Started

## Steps to follow:

1. **Clone the Project Repository**

   ```bash
   git clone https://github.com/Umuzi-org/Sulaiman-Ndlovu-282-node-sql-assignment-javascript.git
   cd Sulaiman-Ndlovu-282-node-sql-assignment-javascript
   ```

2. **Install node modules**

   ```bash
   npm install
   ```

3. **Set Up Environment Variables**

   Create a .env file in the root directory of the project to store your environment variables:

   ```bash
   touch .env
   ```

   Add the following content to the .env file:

   ```env
   DB_USER=user
   DB_PASSWORD=pass
   DB_DATABASE=db
   DB_HOST=localhost
   DB_PORT=5432
   ```

4. **Start the Services with Docker Compose**

   Use Docker Compose to build and start the PostgreSQL and Adminer services:

   ```bash
   docker-compose up -d
   ```

   This command will start two containers:

   - PostgreSQL: The database service running on port 5432.
   - Adminer: A lightweight database management tool accessible at http://localhost:8080.

   ***

   `If you experience any port conflicts`

   Run the following command to get the ID of the running service:

   ```bash
   docker ps -q --filter "expose=8080"
   ```

   Stop the service running at port 8080:

   ```bash
   docker stop <container_id>
   ```

   replace <container_id> with the ID you got from the previous command.

5. **Access Adminer**

   Once the containers are up and running, you can access Adminer by navigating to http://localhost:8080 in your web browser.

   Adminer Login Details:

   - System: `PostgreSQL`
   - listAllVisitors: `db`
   - Username: `user`
   - Password: `pass`
   - Database: `db`

6. **Test the Application on Adminer**

   Now that the application is running, you can interact with it using the Adminer interface. For example, you can:

   - Insert Records: Use the "Insert" tab in Adminer to add new visitors.
   - View Records: Use the "Select" tab to view the list of visitors.
   - Update Records: Use the pencil icon to edit an existing visitor.
   - Delete Records: Use the trash bin icon to remove a visitor.
   - Run Command: Use the "SQL command" tab to run project's commands.

7. **Test the Application on Node**

   To test the application directly in Node.js, follow the steps below to execute each function:

   `Note: These functions are dependent on each other, if you for example try to view a visitor before adding one, you will get an error.`

   1. Create the Visitors Table

      ```javaScript
      const executeCreateTable = async () => {
      const result = await createVisitorsTable();
      console.log(result); // Should log success message if the table is created
      };

      executeCreateTable();
      ```

   2. Add a New Visitor

      ```javaScript
      const executeAddVisitor = async () => {
      const result = await addNewVisitor({
      visitor_name: "Sula Ndlovu",
      visitor_age: 23,
      date_of_visit: "2024-08-06",
      time_of_visit: "18:30",
      assistant_name: "Chris Justine",
      comments: "Enquiry",
      });
      console.log(result); // Should log a new visitor added to the database.
      };

      executeAddVisitor();
      ```

   3. List All Visitors

      ```javaScript
      const executeListVisitors = async () => {
      const visitors = await listAllVisitors();
      console.log(visitors); // Should log the list of all visitors
      };
      executeListVisitors();
      ```

   4. View a Specific Visitor

      ```javaScript
      const executeViewVisitor = async (id) => {
      const visitor = await viewVisitor(id);
      console.log(visitor); // Should log the details of the visitor with the given ID
      };

      executeViewVisitor(1); // Pass the ID of the visitor you want to view
      ```

   5. Update a Visitor's Information

      ```javaScript
      const executeUpdateVisitor = async (id, column, newValue) => {
      const result = await updateVisitor(id, column, newValue);
      console.log(result); // Should log success message if the visitor's data is updated
      };

      executeUpdateVisitor(1, "visitor_age", 25); // Update the visitor's age
      ```

   6. Delete a Visitor

      ```javaScript
      const executeDeleteVisitor = async (id) => {
      const result = await deleteVisitor(id);
      console.log(result); // Should log success message if the visitor is deleted
      };

      executeDeleteVisitor(1); // Pass the ID of the visitor you want to delete
      ```

   7. Delete All Visitors

      ```javaScript
      const executeDeleteAllVisitors = async () => {
      const result = await deleteAllVisitors();
      console.log(result); // Should log success message if all visitors are deleted
      };

      executeDeleteAllVisitors();
      ```

   8. View the Last Added Visitor

      ```javaScript
      const executeViewLastVisitor = async () => {
      const lastVisitor = await viewLastVisitor();
      console.log(lastVisitor); // Should log the last added visitor
      };

      executeViewLastVisitor();
      ```

      **Run All Commands Together**

      ```javaScript
      const executeAll = async () => {
      await createVisitorsTable();
      await addNewVisitor({
      visitor_name: "Sula Ndlovu",
      visitor_age: 23,
      date_of_visit: "2024-08-06",
      time_of_visit: "18:30",
      assistant_name: "Chris Justine",
      comments: "Enquiry",
      });

      await addNewVisitor({
      visitor_name: "Lindo Ndlovu",
      visitor_age: 23,
      date_of_visit: "2024-08-06",
      time_of_visit: "18:30",
      assistant_name: "Marian Justine",
      comments: "Enquiry",
      });

      console.log(await listAllVisitors());
      console.log(await viewVisitor(1));
      console.log(await viewLastVisitor());
      console.log(await updateVisitor(2, "visitor_age", 19));
      console.log(await deleteVisitor(1));
      console.log(await deleteAllVisitors());
      };

      executeAll();
      ```

## Submitting data via the form

1. **Ensure that Docker is still running**

2. **Start the server**

   ```bash
   npm run start
   ```

3. **Access the form in browser**

   - Navigate to: http://localhost:3000/new_visitor

4. **Submit the data**

   - Enter the visitor information and click submit, You should see information saved to the database after submission.

5. **Stopping the Services**

   When you're done, you can stop the Docker containers with:

   ```bash
   docker-compose down
   ```

## Testing the server on terminal

**Note:** If the request is successful, you should see html or json code with no errors.

1.  **Start the server:**

    ```bash
    npm run start
    ```

2.  **Start testing the routes on your terminal using `curl`**

    a. **Test the GET method (`/visitors`)**

    This route retrieves a list of all visitors:

    ```bash
    curl -X GET http://localhost:3000/visitors
    ```

    b. **Test the POST method (`/visitors`)**

    This route creates a new visitor. Make sure to include all the necessary fields:

    ```bash
    curl -X POST http://localhost:3000/visitors \
    -H "Content-Type: application/json" \
    -d '{"visitorName":"John Doe","visitorAge":25,"assistantName":"Jane Doe","dateOfVisit":"2024-11-17","timeOfVisit":"10:00","comments":"Test visitor"}'
    ```

    c. **Test the GET method (`/visitors/:id`)**

    This route retrieves a specific visitor by their `id`:

    ```bash
    curl -X GET http://localhost:3000/visitors/1
    ```

    d. **Test the PUT method (`/visitors/:id`)**

    This route updates a specific visitor's data. You must include the `column` to be updated and its new value:

    ```bash
    curl -X PUT http://localhost:3000/visitors/1 \
    -H "Content-Type: application/json" \
    -d '{"column": "visitor_name", "newValue": "Updated Name"}'
    ```

    e. **Test the DELETE method (`/visitors/:id`)**

    This route deletes a specific visitor by their `id`:

    ```bash
    curl -X DELETE http://localhost:3000/visitors/1
    ```

    f. **Test the DELETE method (`/visitors`)**

    This route deletes all visitors:

    ```bash
    curl -X DELETE http://localhost:3000/visitors
    ```
