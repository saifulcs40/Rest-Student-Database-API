# Student Database API - Testing Documentation

The **Student Database API** is a RESTful service designed to manage student records, including functionalities such as creating, reading, updating, and deleting (CRUD) data. This document provides instructions on how to test the API effectively using tools like Postman and Newman.

## Objective

This document outlines the steps to verify the correctness and reliability of the **Student Database API**. It provides details on how to execute test cases, validate responses, and ensure the API meets expected requirements.

## Key Features to Test

- **Get All Students**: Verify retrieval of all student records.
- **Get a Student by ID**: Ensure that specific student details can be retrieved by ID.
- **Create a New Student**: Confirm that new student entries can be created with valid data.
- **Update Students Technical Skills and Address Details**: Validate that student information can be updated correctly.
- **Delete a Student**: Test if student records can be deleted.

## Testing Tools

- **Postman**: For manual testing and request validation.
- **Newman**: For automated execution of test cases.

## Getting Started with Testing

### Prerequisites

- **Postman**: Download and install [Postman](https://www.postman.com/downloads/).
- **Newman**: For generating reports.
  - Install via npm:
  ```bash
  npm install -g newman
  ```

### How to Set Up

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/student-database-api.git
   ```
2. **Imoprt Postman Collection**
   - Open Postman and import the collection for easy access to all endpoints.
3. **Set Up Environment Variables:**
   - Use environment variables in Postman for `Base URL`
   - Sample environment setup:
     - `baseUrl`: `https://thetestingworldapi.com`

---

### Test Case Scenarios

1. **GET All Students**
   - **Purpose:** To verify that the API retrieves all student records.
   - **Request Type:** `GET`
   - **Endpoint:** `baseUrl/api/studentsDetails`
   - **Expected Response:**
     - Status code `200 OK`
     - The response body should include a list of students in JSON format.
   - **Validation:**
     - Check the response status code.
     - Ensure all student details (ID, First Name, Middle Name, Last Name, Date of Birth) are accurate.
     - Check response time.
2. **GET Specific Student by ID**
   - **Purpose:** To verify retrieval of a specific student by their ID.
   - **Request Type:** `GET`
   - **Endpoint:** `baseUrl/api/studentsDetails/id`
   - **Expected Response:**
     - Status code `200 OK` for valid IDs, `404 Not Found` for non-existing IDs.
     - Correct student details in JSON format.
   - **Validation:**
     - Check the response status code.
     - Ensure the data matches the student with the given ID.
     - Test with valid and invalid IDs.
3. **POST Create a New Student**
   - **Purpose:** To validate that the API correctly handles the creation of new student records.
   - **Request Type:** `POST`
   - **Endpoint:** `baseUrl/api/studentsDetails`
   - **Request Body**
     ```json
     {
       "first_name": "Gerardo",
       "middle_name": "Gaylord",
       "last_name": "Romaguera",
       "date_of_birth": "04/27/2009"
     }
     ```
   - **Expected Response:**
     - Status code `201 Created`
     - The created student's details in the response.
   - **Validation:**
     - Check the response status code.
     - Ensure the new student data appears in subsequent GET requests.
     - Test for missing fields and invalid data formats (e.g., future date for birth date).
4. **POST Create a Technical Skills**
   - **Purpose:** To validate that the API correctly handles the creation of new skill records for the student.
   - **Request Type:** `POST`
   - **Endpoint:** `baseUrl/api/technicalskills`
   - **Request Body**
   ```json
   {
     "id": 10389602,
     "language": ["English", "Bengali"],
     "yearexp": "2 Years",
     "lastused": "Sunday",
     "st_id": "10389602"
   }
   ```
   - **Expected Response:**
     - Status code `201 Created`
     - The created student's details in the response.
   - **Validation:**
     - Check the response status code.
     - Ensure the new student data appears in subsequent GET requests.
5. **POST Create a Student Address**
   - **Purpose:** To validate that the API correctly handles the creation of student address.
   - **Request Type:** `POST`
   - **Endpoint:** `baseUrl/api/addresses`
   - **Request Body**
   ```json
   {
     "Permanent_Address": {
       "House_Number": "123/1",
       "City": "Briatown",
       "State": "Watersport",
       "Country": "Ecuador",
       "PhoneNumber": [
         {
           "Std_Code": "+593",
           "Home": "81-433-3114",
           "Mobile": "32-477-4575"
         },
         {
           "Std_Code": "+593",
           "Home": "58-457-4785",
           "Mobile": "45-478-6979"
         }
       ]
     },
     "stId": 10389602
   }
   ```
   - **Expected Response:**
     - Status code `201 Created`
     - The created student's details in the response.
   - **Validation:**
     - Check the response status code.
     - Ensure the new student data appears in subsequent GET requests.
6. **GET Final Student Details**
   - **Purpose:** To verify retrieval of a specific student details along with the technical skills and address by their ID.
   - **Request Type:** `GET`
   - **Endpoint:** `baseUrl/api/FinalStudentDetails/id`
   - **Expected Response:**
     - Status code `201 Created`
     - Correct student details in JSON format.
   - **Validation:**
     - Check the response status code.
     - Ensure all student details (Language, Year of Experience, House Number, City, Country, Mobile, Current Address) are accurate.

---

### Automate Tests and Generate Report with Newman
For automating the execution of test cases, you can use Newman to run the Postman collection from the command line.

  1. **Run the Tests:**
    ```bash
    newman run Student_Database_Rest_API.postman_collection.json -e Student_DB_API.postman_environment.json
    ```
  2. **View Results:**
    - Check the console output for a summary of passed/failed test cases.
    - Export results to an HTML report if needed:
      ```bash
      newman run Student_Database_Rest_API.postman_collection.json -e Student_DB_API.postman_environment.json -r htmlextra
      ```
---

### Test Result Presentation

