![Rust CLI Binary](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/actions/workflows/cicd.yml/badge.svg)</br>
# IDS-706-Data-Engineering :computer:

## Individual Project 2 :page_facing_up:

## :ballot_box_with_check: Requirements
* __`Rust source code`__: The code should comprehensively understand Rust's syntax and unique features.
* __`Use of GitHub Copilot`__: In your README, explain how you utilized GitHub Copilot in your coding process.
* __`SQLite Database`__: Include a SQLite database and demonstrate CRUD (Create, Read, Update, Delete) operations.
* __`Optimized Rust Binary`__: Include a process that generates an optimized Rust binary as a GitHub Actions artifact that can be downloaded.
* __`README.md`__: A file that clearly explains what the project does, its dependencies, how to run the program, and how GitHub Copilot was used.
* __`GitHub Actions`__: A workflow file that tests, builds, and lints your Rust code.
* __`Video Demo`__: A YouTube link in README.md showing a clear, concise walkthrough and demonstration of your CLI binary.

## :ballot_box_with_check: To-do List
* __Rust Source Code__: Learn to structure Rust source code well and demonstrates a clear understanding of Rust's syntax and unique features.
* __SQLite Database__: Demonstrates CRUD operations on the SQLite database.
* __Use of GitHub Copilot__: Provide the code to install and run the program using GitHub Copilot.
* __Optimized Rust Binary__: Process included that generates an optimized Rust binary as a GitHub Actions artifact that can be downloaded.

## :ballot_box_with_check: Dataset
`flights.csv`
  - This dataset records the number of airline passengers who flew in each month from 1949 to 1960. This dataset has three variables (year, month, and number of passengers).</br>
  - [flights.csv](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/raw/main/rust-cli-binary/flights.csv)</br>
<img src="https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/c26abf40-30d4-44d3-bc32-93e845130fda.png" width="240" height="200"/></br>

## :ballot_box_with_check: Main Progress
#### `Section 1` Rust Source Code with SQLite Database
##### Create Rust source code to perform CRUD operations on an SQLite database.
* `lib.rs`
  - __extract__: Read the CSV file using the file's link.
  - __transform__: Convert the CSV data to a format suitable for the database.
  - __create__: Insert data into the database.
  - __read__:  Retrieve all entries from the database.
  - __update__: Modify existing entries in the database.
  - __delete__: Remove specific entries from the database.
  
      // Check if the result is Ok(()).
          assert!(
              result.is_ok(),
              "Transform function failed with {:?}",
              result
          );
      }
  
      #[test]
      fn test_create() {
          let db_path = "test_flightsDB.db";
  
          // Create data in the database.
          let result = create(db_path, 2023, "March", 200);
          assert!(result.is_ok(), "Create function failed with {:?}", result);
  
          // Verify the created data.
          let conn = Connection::open(db_path).unwrap();
          let passengers: i32 = conn
              .query_row(
                  "SELECT passengers FROM data WHERE year = 2023 AND month = 'March'",
                  params![],
                  |row| row.get(0),
              )
              .unwrap();
          assert_eq!(passengers, 200);
      }
  
      #[test]
      fn test_read() {
          let db_path = "test_flightsDB.db";
  
          let conn = Connection::open(db_path).unwrap();
          conn.execute(
              "CREATE TABLE IF NOT EXISTS data (year INTEGER, month TEXT, passengers INTEGER)",
              [],
          )
          .unwrap();
          conn.execute(              "INSERT INTO data (year, month, passengers) VALUES (2023, 'April', 250)",
              [],
          )
          .unwrap();
  
          // Read data from the database.
          let result = read(db_path);
          assert!(result.is_ok(), "Read function failed with {:?}", result);
      }
  
      #[test]
      fn test_update() {
          let db_path = "test_flightsDB.db";
          let conn = Connection::open(db_path).unwrap();
          conn.execute(
              "CREATE TABLE IF NOT EXISTS data (year INTEGER, month TEXT, passengers INTEGER)",
              [],
          )
          .unwrap();
          conn.execute(
              "INSERT INTO data (year, month, passengers) VALUES (2023, 'May', 300)",
              [],
          )
          .unwrap();
  
          // Update data in the database.
          let result = update(db_path, 2023, "May", 350);
          assert!(result.is_ok(), "Update function failed with {:?}", result);
  
          // Verify the updated data.
          let passengers: i32 = conn
              .query_row(
                  "SELECT passengers FROM data WHERE year = 2023 AND month = 'May'",
                  params![],
                  |row| row.get(0),
              )
              .unwrap();
          assert_eq!(passengers, 350);
      }
  
      #[test]
      fn test_delete() {
          let db_path = "test_flightsDB.db";
          let conn = Connection::open(db_path).unwrap();
          conn.execute(
              "CREATE TABLE IF NOT EXISTS data (year INTEGER, month TEXT, passengers INTEGER)",
              [],
          )
          .unwrap();
          conn.execute(
              "INSERT INTO data (year, month, passengers) VALUES (2023, 'June', 400)",
              [],
          )
          .unwrap();
  
          // Delete data from the database.
          let result = delete(db_path, 2023);
          assert!(result.is_ok(), "Delete function failed with {:?}", result);
  
          // Verify the data was properly deleted.
          let count: i32 = conn
              .query_row(
                  "SELECT COUNT(*) FROM data WHERE year = 2023",
                  params![],
                  |row| row.get(0),
              )
              .unwrap();
          assert_eq!(count, 0);
      }
  }
  ```

#### `Section 2`  Viewing the Results of the Rust Source Code
##### Verify the CRUD Operations on the SQLite Database Using Rust
