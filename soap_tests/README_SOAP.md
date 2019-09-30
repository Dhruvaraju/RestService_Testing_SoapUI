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



