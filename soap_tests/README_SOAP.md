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


