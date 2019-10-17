# RestService_Testing_SoapUI
Testing REST api's with soap ui and automating them.

### Webservice?
- Medium of communication between couple of applications or devices via world wide web (www).

### REST (Representational State Transfer)
- Rest mainly uses JSON for data transfer
- Follows Stateless transfer
- Uses standard HTTP methods GET, POST, DELETE, UPDATE, PUT
- Lightweight alternative to SOAP

### REST Service calls
- REST calls are simple http calls
- A Rest call contains 3 parts (very broad description)
-[x] Base URL
-[x] Resources
-[x] Parameters
    - Query parameters
    - Path Parameters
    - Request body parameters

### HTTP Methods

#### GET
- Used to extract information from a URL - Target resource.
- Will not alter the data, No other effect on data or target resource, only retrieval
#### POST
- Used to send data to update in the server, like Customer details update.
#### PUT
- To update details or data on target resource.
- Replaces all the current representation of target resource with uploaded content.
#### DELETE
- Used to remove particular information from target resource.
- Removes all current representation of the target resource given by URL.

### Example of a Rest call
- We can consider google search as a simple http get call

```
https://www.google.com/search?ei=HlabXf-DMKWMmgfdyqtY&q=soapui&oq=soapui&gs_l=psy-ab.3..0i356l4.0.0..3322761...0.2..0.0.0.......0......gws-wiz.aSb35rkJ4ms&ved=0ahUKEwj_it32t4rlAhUlhuYKHV3lCgsQ4dUDCAo&uact=5

Base URL: https://www.google.com
Resource : /search
Parameters: ?ei=HlabXf-DMKWMmgfdyqtY&q=soapui&oq=soapui&gs_l=psy-ab.3..0i356l4.0.0..3322761...0.2..0.0.0.......0......gws-wiz.aSb35rkJ4ms&ved=0ahUKEwj_it32t4rlAhUlhuYKHV3lCgsQ4dUDCAo&uact=5

```
Parameters in example:

Name | Value | Type
--------|--------------------------------------------------|--------------
ei | HlabXf-DMKWMmgfdyqtY | Query
q | soapui | Query
oq | soapui | Query
gs_l | psy-ab.3..0i356l4.0.0..3322761...0.2..0.0.0.......0......gws-wiz.aSb35rkJ4ms | Query
ved | 0ahUKEwj_it32t4rlAhUlhuYKHV3lCgsQ4dUDCAo | Query
uact | 5 | Query

> Here the target resource is google's **Search** api.

### Example REST API
- we will consider an imaginary pet store for our REST testing
- http://petstore.swagger.io/
- REST apis are documented by a file called swagger.
- An example swagger is present in REST_TESTS >> swagger.files folder with name petStore_example_REST.json
- import this swagger to Soap-ui project >> import swagger >> click on generate WADL 
- With WADL you can import all the URL at a single instance

### Pet store example 

> Open the JSON file in swagger editor or navigate to URL http://petstore.swagger.io/ 
> This location will explain the service, URLs we need to use to access them and resources and parameters that are required to access it.

- Pet store has 3 APIs:
#### Pet - Provides details about pet

URL | HTTP Method  | Description 
--------------------|------------------------|---------------------
/pet | POST | Add a new pet to store
/pet | PUT | Update an existing pet
/pet/findbystatus | GET | Lists pets by status
/pet/{petId} | GET | Find a pet by Id
/pet/{petId} | POST | Updates a pet in the store with form data
/pet/{petId} | DELETE | Deletes a pet from store
/pet/{petId}/uploadImage | POST | Uploads an image

#### Store - Provides details about inventory

URL | HTTP Method  | Description 
--------------------|------------------------|---------------------
/store/inventory | GET | Returns pet inventories by status
/store/order | POST | Place an order for a pet
/store/order/{orderId} | GET | Find purchase order by ID
/store/order/{orderId} | DELETE | Deletes a purchase order by Id

#### User - User Access management

URL | HTTP Method  | Description 
--------------------|------------------------|---------------------
/user | POST | Creates a user
/user/createWithArray | POST | Creates list of users with given input array
/user/createWithList | POST | Creates list of users with given input array
/user/login | GET | Logs in a user
/user/logout | GET | Logs out a user
/user/{userName} | GET | Get user by username
/user/{userName} | PUT | Update user
/user/{userName} | DELETE | Delete User

> We can test this resources now, By adding the JSON input but we cannot run assertions.
> To run assertions on this resources we need to create test suite and test cases

### Creating a test suite and test case from imported swagger
- Right Click on Imported swagger >> Click on Generate Test suite >> A pop up will appear
- Select One test case for each resource if we want to test each resource separate.
- Select Single Test Case with one request for each method, if you want to test all in a single test case or you want to automate them
- Select all resources by clicking select all and click ok

### Create TestSuite, TestCase and TestStep from project
- Right Click on project >> Select New TestSuite >> Name It >> click Ok
- Right Click on Test suite >> Select New TestCase >> Name it >> Click Ok
- Right Click on TestSuite >> Select Add step >> RestRequest >> Name it >> Pop up appears select appropriate REST Resquest >> Click Ok

> Group of TestSteps called as TestCase.
> Group of TestCases called as TestSuite.
> Group of TestSuites called as Project.

- Created a testsuite named alphaTest, testCase as userTest and added testStep create user by selecting /user post resource.

### Simple Assertions
#### Creating User
To make the user POST called added the below request json in media type and click on the play button, It will show status as 200.

```
{
  "id": 9410102019,
  "username": "dexter",
  "firstName": "dexter",
  "lastName": "morgan",
  "email": "dexter@test.com",
  "password": "dextermorgan",
  "phone": "3899834567",
  "userStatus": 0
} 
```

#### Getting User Details
- To get the above added user details added a new test step with /user/{userName} get request named it getuser.
- In the request tab you will see a template variable add value as dexter to get the user details.
- Template means the variable present is a path parameter.

### Basic Assertions
- To add an assertion, click on the '+' symbol beside your URL
- Once you add assertion it runs and in assertion tab it turns green if it is sucessful, turns to red if it fails.
- We can edit assertion by double clicking on the assertion, in the assertion tab.

#### Contains assertion
To check if the response contains specific test
- Property Content >> Select Contains >> Add >> Provide text you want to check >> click ok
- Added check to see if '0' is available in the response.
- **Not Contains** assertion working in the same way, provide the text which should not be in response.
- Added not contains assertion to check that 'failed' is not in the response.

#### Compliance Status and Standards assertions
##### Valid http Code assertion
- Checks if the status code returned in response is equal to the one provided.
- Compliance Status >> Valid HTTP Status Codes >> Provide the status code in pop up >> Click Ok // Check for 200 added

##### InValid http status code assertion
- Checks if the status code returned in response is not equal to the one provided.
- Compliance Status >> Invalid HTTP Status codes >> Provide status code in popup >> click ok //Check for 400 added

##### Schema compliance
- Checks if the response object returned is a compliant schema with the WADL generated from swagger
- Compliance Status >> Schema Compliance >> Pop up to compare WADL >> click ok

##### SLA assertion 
- Checks if the response is returned in amount of milliseconds provided
- SLA >> Response SLA >> Provide time in milliseconds >> click Ok

### JSONPath Match Assertion
- Checks the value of a certain JSON path with value provided
- We have 2 notations to give JSON paths
  - Dot Notation
  - Bracket Notation


Example Json:
```
{
   "id": 49001,
   "category":    {
      "id": 4001,
      "name": "Domestic"
   },
   "name": "Dogs",
   "photoUrls": ["NA"],
   "tags": [   {
      "id": 9001,
      "name": "Low Cost"
   }],
   "status": "available"
}
```

We can get id from tags attribute in 2 ways:
- Dot Notation: ``` $.tags[0].id ```
- Bracket Notation: ``` $['tags'][0]['id'] ```

### Properties project level, Test Suite Level, Test Case Level getting them.
- Project Level
    - Click on project >> Bottom left side we will be able to see properties, beside it custom properties will be available
    - We can add a variable and assign it a value by clicking '+'
    - To access project level variables ${#Project#propertyname} 
    ``` ${#Project#ProjectProperty} will fetch the 'This_is_project_property' ```
- Test Suite Level
    - Click on TestSuite >> custom Properties >> Add properties
    - To Access TestSuite Property ${#TestSuite#Property} 
    ``` ${#TestSuite#TestSuiteProperty} return 'This_is_testSuite_property' ```
- Test case Level
    - Click on TestSuite >> custom Properties >> Add properties
    - To Access TestCase Property ${#TestCase#Property}  
    ``` ${#TestCase#TestCaseProperty} return 'This_is_TestCase_property' ```

### Automating Rest Tests

> Test automation is done using groovy script in Soap UI.

- Groovy scripts can be done in 2 ways
    - By adding a new test step as groovy-script
    - By adding a script assertion

### By using New test Step as Groovy Script
- Add a new test case >> Add a new Test Step >> Groovy Script
- This will be invoked with 3 variables
    - log
    - Context
    - TestRunner

### Log
- Log is used to print information in console
- you can invoke console logging from script step editor as log.info('Your Message')
``` log.info('Test script Initiation') ```
### Context
- Context is used to fetch test case level properties.
- Scope of context is testcase.
- Syntax for fetching context variables context.expand('${#TestCase#initialValue}');
``` log.info ('Value of Test case level variable initialValue is : '+context.expand('${#TestCase#initialValue}')); ```
### TestRunner
- TestRunner can access all properties in a project
- TestRunner Scope is project.
- Any property testSuite level, Testcase level, test step level, project level can be accessed
    - But while accessing property values we need to follow hierarchy 
    - Project >> TestSuite >> TestCase >> TestStep
- How to access a testcase property from script is explained below
    - Initially we will declare testRunner then we have to state current location  //testRunner.testCase
    - Since we have to get property from another testCase we need to access it parent element testSuite // testRunner.testCase.testSuite
    - from testSuite get hold of the testCases array and get the testCase by its name  //testRunner.testCase.testSuite.testCases["testcasename"]
    - Finally fetch the property by invoking getPropertyValue like getPropertyValue("propertyname")
```
testRunner.testCase.testSuite.testCases["userTest"].getPropertyValue("TestCaseProperty");
testRunner.testCase.testSuite.testCases['userTest'].getPropertyValue('TestCaseProperty'); // Single quote or double both works
```
- For Setting property to a test case use setPropertyValue('propertyName','PropertyValue');
```
testRunner.testCase.testSuite.testCases['userTest'].setPropertyValue('setFromScript','IamFromScript');
```
Fetching the request of a test case:
- Request is a property  for the test case we can get it by getting the 'Request' property of a test step.
```
testRunner.testCase.testSuite.testCases['userTest'].testSteps['createUserPost'].getPropertyValue('Request');
```
### Defining variables in groovy script
- keyword 'def' id used to initiate a variable in groovy script
```
def userTest = testRunner.testCase.testSuite.testCases['userTest']; // now we can use addTest to extarct properties from it.
```
### Getting, Setting project variables:
```
def project = testRunner.testCase.testSuite.project;
project.setPropertyValue('author','dexter');
project.getPropertyValue('author');
```
