# Project Title
wso2-api-sample is a wso2 project with an api which can take  GET, POST, PUT, DELETE with json payload.This is a bibliographic REST service which fetches, creates, updates and deletes books from the store.  Request payload is validated against a json schema transformed to xml and xslt adds required namespace. The xml will be sent to back end SOAP mock service. Response from SOAP mock service is transformed to json and will be returned to the client.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites
Install Oracle Java SE Development Kit (JDK) version 1.8.* and set the JAVA_HOME environment variable
Install SOAPUI
Instsall maven

### Installing

Install Developer Studio Kernel with pre-packaged Eclipse

1. Go to https://wso2.com/products/developer-studio/
2. Go to “More Downloads”
3. Download the .zip for Mac 64bit
4. unzip and copy the eclipse folder into your workspace. For example to /<workspace_dir>/eclipse/luna/
5. Now go to /<workspace_dir>/eclipse/luna/Eclipse.app/Contents/MacOS/ and grant permission to eclipse app (This is only required only for Mac and only once) using the following command
    1. chmod +x eclipse
6. Now from /<workspace_dir>/eclipse/luna/Eclipse.app/Contents/MacOS/ run the following command to start eclipse with Developer Studio
    1. ./eclipse


Installing WSO2 Enterprise Integrator
1. Download Enterprise Integrator installer from https://wso2.com/integration/install/
2. Install Enterprise Integrator using the downloaded installer.
3. In MacOS, by default Enterprise Integrator will be installed to /Library/WSO2/EnterpriseIntegrator/

Install WSO2 API Manager
1. Download WSO2 API Manager installer from https://wso2.com/api-management/install/
2. Install the API Manager using the downloaded installer.
3. In MacOS, API Manager will be installed to /Library/WSO2/APIManager/
4. If we are installing and running multiple WSO2 products on same server then we must change their default ports with an offset value to avoid port conflicts.(Refer https://docs.wso2.com/display/AM1100/Changing+the+Default+Ports+with+Offset)
    1. There are two ways to set an offset to a port:
        1. Pass the port offset to the server during startup. The following command starts the server with the default port incremented by 3:./wso2server.sh -DportOffset=3
        2. Set the Ports section of <PRODUCT_HOME>/repository/conf/carbon.xml. E.g., <Offset>3</Offset>
5. Start the API Manager from /Library/WSO2/APIManager/2.6.0/bin/wso2server.sh
6. Log into API Manager https://192.168.0.25:9446/publisher and load the created REST API by using the swagger file generated from Enterprise Integrator.


##DEPLOYEMENT
1.Open SOAPUI and import the mock soap service soap-mock/BiblioSOAP-soapui-project.xml and start the mock server 
1.copy the biblio-distribution/target/biblio-distribution_1.0.0.car into <EI_HOME>/repository/deployment/server/carbonapps/
2.Start EI from /Library/WSO2/EnterpriseIntegrator/6.4.0/bin/integrator.sh
3.Log into Enterprise Integrator Management Console(https://localhost:9443/carbon/) and check the API in the Management Console and note the API url (http://192.168.0.25:8280/biblio/titles)
4.Start the API Manager <AM_HOME>/bin/wso2server.sh
5.Open API Publisher url and Create the API using the supplied swagger file.
6.Open API Store and go to API Console to invoke the api and to see the response

## Running Tests

1. Import SOAPUI tests into SOAP UI using the supplied soapui-tests/BiblioServiceSoapUITests-soapui-project.xml

2. Run the biblio-api-TestSuite

## Sample Request
{
    "Title": {
      "ISBN": "9876543219876",
      "Author": "Erle Stanley Gardner",
      "TitleName": "The Case of the Amorous Aunt",
      "PublishDate": "03-03-1963",
      "Price": 3.49,
      "Quantity": 20
    }
  
}

## Sample Response
{
    "CreateTitlesResponse": {
        "Title": {
            "ISBN": 9876543219876,
            "Author": "Erle Stanley Gardner",
            "TitleName": "The Case of the Amorous Aunt",
            "PublishDate": "03-03-1963",
            "Price": 3.49,
            "Quantity": 20
        }
    }
}
