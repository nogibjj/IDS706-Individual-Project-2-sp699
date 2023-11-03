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
 
#### `Section 2` Install Dependencies
##### Install the dependencies for Rust configuration.
* For the installation of dependencies required for Rust configuration, the dependencies used in the Rust files are listed in the Cargo.toml file, and 'cargo release' is utilized for their installation.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/ec4e7d2c-71f1-4145-a8d6-fb57d6a16165)
#### `Section 3` Optimized Rust Binary
##### Rust binary that has been compiled in an optimized form.
* A process has been established using GitHub Actions to automate the building and storage of the Rust binary. With 'release' utilized for the build, the binary is then made available for download at the 'rust-cli-binary/target/release/rust-cli-binary' path.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/51b9e45c-aa07-4e51-8416-c119848c4f48)
#### `Section 4` GitHub Copilot
##### Use of GitHub Copilot
* How to utilize GitHub Copilot in coding process
  - Ask about the coding when writing the Rust CRUD file.
  - Inquire about why the code isn't running.
  - Seek assistance with setting up GitHub configuration.
#### `Section 5` GitHub Actions
##### Test, Build, and Lint Rust Code
* Using the __`cargo`__ command, the GitHub Actions file can test, build, and lint your Rust code effectively.
1. __`Test`__
  - Test the SQLite CRUD operation using Rust.
  - Use the `cargo test` for testing.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/221630b9-2793-4b2d-b444-83a7a05e620a)

2. __`Build`__
  - Build the Rust code in the current directory.
  - `cargo build` compile the code and produce an executable binary or library.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/58c23eaa-ecc3-431b-bbee-0174fbda8494)

3. __`Lint`__
  - Check Rust code for style guidelines, conventions, and potential errors or issues.
  - Use `cargo clippy --quiet`.
  - '--quiet' helps get only the resulting errors and warnings displayed without any additional output.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/09538eab-00b7-474d-8da4-22d42e118b40)

#### `Section 6` Result of Rust Performance
##### See the result of the rust code.
* When executing `cargo run`, the successful processing of the CRUD operations can be observed.

1. __`cargo run`__: This command triggers the extraction of a 'csv' file from its source link, followed by its transformation into a database file compatible with SQLite.

<img src="https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/509229cc-ab48-4458-a38e-a3a32054d0e4.png" width="700" height="80"/>

2. __`Create`__: The entry '2023, October, 800' has been successfully inserted into the SQLite database.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/d6683cab-7d01-427b-bce7-34b89117ba3e) </br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/c2859599-b9d3-4fab-8f77-cabd7c1d7fda)

3. __`Read`__: The entire contents of the database can be viewed through the read operation.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/b3417ad4-10f8-45fc-a364-1afe42c67cd6)

4. __`Update`__: The data '2023, October, 800' has been updated to '2023, October, 1000' in the database.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/f976f0b5-093c-4c45-9e3a-930b4c359d94)</br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/75459e13-ef40-4d72-9aae-56ebdcc0eb3d)

5. __`Delete`__: The entry '2023, October, 1000' has been deleted, and you will see that it is no longer present in the database.

![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/7ea4efa0-6249-4504-aa7d-0ed081437afc)</br>
![image](https://github.com/nogibjj/IDS706-Individual-Project-2-sp699/assets/143478016/7f3a2e0d-c53d-4763-ac8c-32abfaa37311)

## :ballot_box_with_check: Demo Video
The entire process of configuring the Rust CLI Binary is explained in a demo video available at the following link. _(To be updated)_
