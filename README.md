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
* `main.rs`
  - Extract the CSV file, convert it to a database file, and then perform CRUD operations using it.
* `test.rs`
  - Test all the functions in 'lib.rs' and verify that the operations execute correctly.

#### `Section 2` Optimized Rust Binary
##### Rust binary that has been compiled in an optimized form.
* 

#### `Section 3` GitHub Copilot
##### Use of GitHub Copilot
* How to utilize GitHub Copilot in coding process
  - Ask about the coding when writing the Rust CRUD file.
  - Inquire about why the code isn't running.
  - Seek assistance with setting up GitHub configuration.

#### `Section 4` GitHub Actions
##### Test, Build, and Lint Rust Code
* Using the __`cargo`__ command, the GitHub Actions file can test, build, and lint your Rust code effectively.
1. Test
  - Test the SQLite CRUD operation using Rust.
  - Use the 'cargo test' for testing.</br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/221630b9-2793-4b2d-b444-83a7a05e620a)
2. Build
  - Build the Rust code in the current directory.
  - 'cargo build' compile the code and produce an executable binary or library.</br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/58c23eaa-ecc3-431b-bbee-0174fbda8494)
3. Lint
  - Check Rust code for style guidelines, conventions, and potential errors or issues.
  - Use 'cargo clippy --quiet'.
  - '--quiet' helps get only the resulting errors and warnings displayed without any additional output.</br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/09538eab-00b7-474d-8da4-22d42e118b40)

