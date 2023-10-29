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
  ```Rust
  use rusqlite::{params, Connection, Result};
  use std::fs::File;
  use std::io::Write;
  
  pub fn extract(url: &str, file_path: &str) -> Result<(), Box<dyn std::error::Error>> {
      // Fetch data from the URL via an HTTP request.
      let response = reqwest::blocking::get(url)?;
  
      // Read the content of the fetched data.
      let content = response.text()?;
  
      // Create a file at the specified path and write the content.
      let mut file = File::create(file_path)?;
      file.write_all(content.as_bytes())?;
  
      Ok(())
  }
  
  pub fn transform(csv_path: &str, db_path: &str) -> Result<(), Box<dyn std::error::Error>> {
      // Open the CSV file.
      let mut rdr = csv::Reader::from_path(csv_path)?;
  
      // Create or connect to an SQLite database file.
      let conn = Connection::open(db_path)?;
  
      // Create the appropriate table. This example assumes a simple structure.
      // Adjust the table structure according to your actual use case.
      conn.execute(
          "CREATE TABLE IF NOT EXISTS data (year INTEGER, month TEXT, passengers INTEGER)", 
          [],
      )?;
  
      for result in rdr.deserialize() {
          let (year, month, passengers): (i32, String, i32) = result?;
          conn.execute(
              "INSERT INTO data (year, month, passengers) VALUES (?1, ?2, ?3)",
              params![year, month, passengers],
          )?;
      }
  
      Ok(())
  }
  
  pub fn create(
      db_path: &str,
      year: i32,
      month: &str,
      passengers: i32,
  ) -> Result<(), Box<dyn std::error::Error>> {
      // Connect to the SQLite database file.
      let conn = rusqlite::Connection::open(db_path)?;
  
      // Insert data into the `data` table.
      conn.execute(
          "INSERT INTO data (year, month, passengers) VALUES (?1, ?2, ?3)",
          params![year, month, passengers],
      )?;
  
      println!("Data successfully created into the database.");
  
      Ok(())
  }
  
  pub fn read(db_path: &str) -> Result<(), Box<dyn std::error::Error>> {
      // Connect to the SQLite database file.
      let conn = rusqlite::Connection::open(db_path)?;
  
      // Execute the query and fetch the results.
      let mut stmt = conn.prepare("SELECT year, month, passengers FROM data")?;
      let rows = stmt.query_map([], |row| {
          Ok((
              row.get::<_, i32>("year")?,
              row.get::<_, String>("month")?,
              row.get::<_, i32>("passengers")?,
          ))
      })?;
  
      // Print the results.
      for row_result in rows {
          let (year, month, passengers) = row_result?;
          println!("{}, {}, {}", year, month, passengers);
      }
  
      Ok(())
  }
  
  pub fn update(
      db_path: &str,
      year: i32,
      month: &str,
      passengers: i32,
  ) -> Result<(), Box<dyn std::error::Error>> {
      // Connect to the SQLite database file.
      let conn = rusqlite::Connection::open(db_path)?;
  
      // Update the number of passengers for the specified year and month.
      let rows_modified = conn.execute(
          "UPDATE data SET passengers = ?3 WHERE year = ?1 AND month = ?2",
          params![year, month, passengers],
      )?;
  
      if rows_modified == 0 {
          println!("No data found for the specified year and month.");
      } else {
          println!("Data successfully updated in the database.");
      }
  
      Ok(())
  }
  
  pub fn delete(db_path: &str, year: i32) -> Result<()> {
      let conn = Connection::open(db_path)?;
  
      conn.execute("DELETE FROM data WHERE year = ?1", params![year])?;
  
      Ok(())
  }
  ```

* `main.rs`
  - Extract the CSV file, convert it to a database file, and then perform CRUD operations using it.
  ```Rust
  use rust_cli_binary::{extract, transform, create, read, update, delete};
  use std::fs;
  
  fn main() {
      // Delete the database file.
      let _ = fs::remove_file("flightsDB.db");
  
      extract(
          "https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/raw/main/rust-cli-binary/flights.csv",
          "flights.csv",
      )
      .unwrap();
  
      let csv_path = "flights.csv";
      let db_path = "flightsDB.db";
      match transform(csv_path, db_path) {
          Ok(_) => println!("CSV file has been successfully converted to SQLite DB."),
          Err(e) => println!("An error occurred during conversion: {}", e),
      }
  
      match create("flightsDB.db", 2023, "October", 800) {
          Ok(_) => println!("Successfully inserted data into the SQLite DB."),
          Err(e) => println!("Error occurred while inserting data: {}", e),
      }
  
      match read("flightsDB.db") {
          Ok(_) => println!("Successfully read from the SQLite DB."),
          Err(e) => println!("Error occurred while reading data: {}", e),
      }
      
      println!();
  
      match update("flightsDB.db", 2023, "October", 1000) {
          Ok(_) => println!("Successfully updated data in the SQLite DB."),
          Err(e) => println!("Error occurred while updating data: {}", e),
      }
  
      match read("flightsDB.db") {
          Ok(_) => println!("Successfully read from the SQLite DB."),
          Err(e) => println!("Error occurred while reading data: {}", e),
      }
      
      println!();
  
      let year_to_delete = 2023;
      match delete(db_path, year_to_delete) {
          Ok(_) => println!("Successfully deleted data for year {}.", year_to_delete),
          Err(e) => println!("An error occurred: {}", e),
      }
  
      match read("flightsDB.db") {
          Ok(_) => println!("Successfully read from the SQLite DB."),
          Err(e) => println!("Error occurred while reading data: {}", e),
      }
      
      println!();
  }
  ```

* `test.rs`
  - Test all the functions in 'lib.rs' and verify that the operations execute correctly.
  ```Rust
  #[macro_use]
  extern crate lazy_static;
  
  #[cfg(test)]
  mod tests {
      use rusqlite::params;
      use rusqlite::Connection;
      use rust_cli_binary::{create, delete, extract, read, transform, update};
      use std::fs;
      use std::sync::Once;
  
      lazy_static! {
          static ref INIT: Once = Once::new();
      }
  
      #[test]
      fn test_extract() {
          // Define test URL and save path.
          let test_url = "https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/raw/main/rust-cli-binary/test_flights.csv"; // This URL is an example. Please replace with an actual accessible URL.
          let test_path = "test_flights.csv";
  
          // Execute the extract function.
          let result = extract(test_url, test_path);
  
          // Check if the result is Ok(()).
          assert!(result.is_ok(), "Extract function failed with {:?}", result);
  
          // Check if the file was actually created.
          assert!(
              fs::metadata(test_path).is_ok(),
              "Failed to create the file at {}",
              test_path
          );
      }
  
      #[test]
      fn test_transform() {
          // Create sample CSV data.
          let csv_path = "test_flights.csv";
          let db_path = "test_flightsDB.db";
  
          // Execute the transform function.
          let result = transform(csv_path, db_path);
  
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
          conn.execute(
              "INSERT INTO data (year, month, passengers) VALUES (2023, 'April', 250)",
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
