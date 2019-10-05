# RestService_Testing_SoapUI
Testing SOAP api's with soap ui and automating them.

Webservice?
- Medium of communication between couple of applications or devices via world wide web (www).

- SOAP (Simple object access protocol)
    - Soap mainly interacts with systems with an XML called as soap message
    - Soap Message https://www.ibm.com/support/knowledgecenter/en/SSMKHH_10.0.0/com.ibm.etools.mft.doc/ac55780_.htm
    - WSDL (Web Services Description language), Description of a webservice is provided in this document.
    - WSDL is know as service description, Describing location of the service, operations done.
    - SOAP message is date that you transfer, WSDL is description of your service.
    - Example for SOAP wbservice 
        - http://www.dneonline.com/calculator.asmx
        - For WSDL: http://www.dneonline.com/calculator.asmx?WSDL
        - For SOAP Message - http://www.dneonline.com/calculator.asmx?op=Divide

Testing a SOAP service example of calculator service:
- Once opening SOAPUI
- Goto File >> New SOAP Project >> A popup will appear
- provide a project name >> enter the url for WSDL path >> check create sample requests for all operations >> click ok
- SOAPUI will scan the wsdl and generate the requests for us.
- Expand each operation, request will be available, double click on it and we can add paramaters and test them.
- Update parameters and click on the play button on request tab, result will come in xml and a raw format.
- XML format will give the response as soap object, while raw data will present all other details like status code few other attributes.

Creating a testsuite and testcase
- Right click on the project and click on New Test Suite name it as your projecct name
- Right click on the test suite and click on new test case and add your functinality name
- Under test case right click on test step and add a new step

Adding test step
- Once you click on add new test step it will show what request need to be added
- Select Soap request and name it as you wish
- Select the request from dropdown and check add soap response assertion and  create optional elements >> click ok

Group of test steps are called test cases
Group of test cases are called test suite
Group of test suites are called project

Basic Assertions:
- Double click on the test step to open it, you will see a '+' symbol beside the play button use it to add assertions.
- Check for a cetain text, like check for AddResult in your response
    - Click on add assertion >> property content >>  select contains and click add
    - it will as for content provide text there eg: AddResult and click ok, it will run the assertion and say it got passed
- Check for not contains a specific string eg: error
    - Add Assertion>> Property Content >> Not Contains click add >> provide your text >> click ok
- Check for valid SOAP message
    -  Add Assertion >> Compliance, Status , Standards >> SOAP Response >> click add >> it verifies and provides result
- Check for valid HTTP code
    - Add Assertion >> Compliance Status and Standards >> Valid HTTP Status Codes >> Add >> Enter Status code >> ok >> Runs asertion
- Check for Response time
    - Add Assertion >> SLA >> Response SLA >> Add >> Enter time in milliseconds >> ok >> Runs Assertion

Advanced Assertions:
- Check sum of 56 and 44 through xpath
    - Add Assertion >> Property Content >> Xpath Match >> Add >> Xpath match configuration appears
    - Click Declare which is below xpath expressions, it will declare all the xpath's namespaces
    - start your xpath with '//' parent node / child node / ... / your node
    - example:
    Response : 
    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Body>
      <AddResponse xmlns="http://tempuri.org/">
         <AddResult>100</AddResult>
      </AddResponse>
    </soap:Body>
    </soap:Envelope>

    Xpath will be:
    declare namespace ns1='http://tempuri.org/';
    declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
    //ns1:AddResponse/ns1:AddResult

    Or Xpath can be as:
    declare namespace ns1='http://tempuri.org/';
    declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
    declare namespace xsi="http://www.w3.org/2001/XMLSchema-instance";
    declare namespace xsd="http://www.w3.org/2001/XMLSchema";
    //ns1:AddResponse/ns1:AddResult
    - Provide the expected result in the expected result tab here it will be 100

    Check for node existance:
    - Add Assertion >> Property Content >> Xpath Match >> Add >> Xpath match configuration appears
    - declare name spaces >> use exists function like 'exists(//ns1:AddResult)'
    - in expected value section provide true if node exists else false
    example:
    declare namespace ns1='http://tempuri.org/';
    declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
    exists(//ns1:AddResult)

    Check number of nodes in a response:
    - Add Assertion >> Property Content >> Xpath Match >> Add >> Xpath match configuration appears
    - declare name spaces >> use count function like 'count(//ns1:AddResult)'
    - in expected value section provide number that you are expecting to get
    example:
    declare namespace ns1='http://tempuri.org/';
    declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
    count(//ns1:AddResult) in expected tab give 1

    To Execute all test cases:
    - Double click on testesuite and click play button, it will run all the test cases and show results
Properties project level, Test Suite Level, Test Case Level getting and setting them.
- Project Level
    - Click on project >> Bottom left side we will be able to see properties, beside it custom properties will be available
    - We can add a variable and assign it a value by clciking '+'
    - To access project level variables ${#Project#Variablename} eg: ${#Project#adminUser} will fetch Dexter in attached project
- Test Suite Level
    - Click on TestSuite >> custom Properties >> Add properties
    - To Access TestSuite Property ${#TestSuite#Property} eg: ${#TestSuite#varOne} return 25
- Test case Level
    - Click on TestSuite >> custom Properties >> Add properties
    - To Access TestCase Property ${#TestCase#Property} eg: ${#TestCase#egProperty} return TestData

Adding Data in reguest:
- To add data in request nodes simple add the syntax as mentioned above
- We can alos add data by right click in the node text area >> GetData >> which which var you want
- SoapUi will generate the syntax for us

Placing all properties data in a single place:
- To add properties in a single, file right click on testcase >> add Step >> Properties
- in the properties tab you can add all properties what you need 
- Syntax for refering them ${Properties#Propertyname} or you can choose from get data.
- We can rename the properties step to any thing eg: PropData then syntax will be ${PropData#Propertyname}

Properties upload from external file:
- Create a file with .properties as extention
- go to custom properties >> click on load properties from external file
- Example properties file is added in the project

Properties transfer from one test step to others
//Adding the response from one service as input in request of another service

Example for Property Transfer consider the following senario:
//We will add 2 numbers, take the sum
//Pass the sum to substration first variable and substract 5
// send the substraction result to Multiplication, multiply it with 5
// Send the result to division and devide it by 10

Add property transfer:
- Right Click on Test case >> add Step >> Property transfer >> name it as you want
- In property transfer window click + for adding a property to be transfered
- Select the Source test step from dropdown >> select property Response >> Path Language as Xpath
- Similarly select the target test step >> select Property ad request >> path language as xpath
- now click on the small 'ns' to add namespace in both
- now define xpath for the values

eg response: 
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <soap:Body>
      <AddResponse xmlns="http://tempuri.org/">
         <AddResult>61</AddResult>
      </AddResponse>
   </soap:Body>
</soap:Envelope>

eg request:
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
   <soap:Header/>
   <soap:Body>
      <tem:Subtract>
         <tem:intA>?</tem:intA>
         <tem:intB>?</tem:intB>
      </tem:Subtract>
   </soap:Body>
</soap:Envelope>

We need to add the AddRessult value from response to tem:intA in response
eg Source Xpath:
declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
declare namespace ns1='http://tempuri.org/';
//ns1:AddResponse/ns1:AddResult/text()

eg Target Xpath:
declare namespace soap='http://www.w3.org/2003/05/soap-envelope';
declare namespace ns1='http://tempuri.org/';
//ns1:Subtract/ns1:intA

****** Note: Even if we have something appended to node we need to prefix it with namespace eg: tem:intA defined as ns1:intA

Automating test Scritps:
Introduction to Groovy:
- Create a new project with all tests in a single test case name it as automation_soap
- create a new test suite create test cases to do all arthematic operations
- we can add script as a step to any of the test case or we can create a new testcase and add only script
- right click on test suite >> new test case >> name it >> add step >> groovy script
- scripts are invoked with log, context and test runner variables

Groovy Script Variables: (To run groovy scripts just click play button on the editor)
- Log is used to print infromation in console
    - you can invoke console logging from script step editor as log.info('Your Message')
    - eg: log.info('Test script Initiation')
- Context is used to fetch test case level properties, hence context scope is testcase
    - Syntax for fetching context variables context.expand('${#TestCase#initialValue}');
    - we can log it as log.info ('Value of Test case level variable initialValue is : '+context.expand('${#TestCase#initialValue}'));
- testRunner is used to access all properties in a project
    - Any property testSuite level, Testcase level, teststep level, project level can be accessed
    - But while accessing we need to follow the hierachy 
    - Project >> TestSuite >> TestCase >> TestStep
    - eg: we are trying to get add testcase property from script it is explained below
    - Initially we will declare testRunner then we have to state current location  //testRunner.testCase
    - Since we have to get property from another testCase we need to access it parent element testSuite // testRunner.testCase.testSuite
    - from testSuite get hold of the testCases array and get the testCase by its name  //testRunner.testCase.testSuite.testCases["add"]
    - Finally fetch the property by invoking getPropertyValue like getPropertyValue("addProperty001")
    eg: testRunner.testCase.testSuite.testCases["add"].getPropertyValue("addProperty001");
        testRunner.testCase.testSuite.testCases['add'].getPropertyValue('addProperty001'); // Single quote or double both works