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
- Will not alter the data, No other effect on data or target resource, only retrival
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