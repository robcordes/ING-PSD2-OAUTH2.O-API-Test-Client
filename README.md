# ING-PSD2-APi-Test-Client
This is a Postman collection and environment one can use to experiment with and to obeserve the workings of the ING PSD2 OAuth 2.0 interfaces

The request Sideload Jrsassign-js loads the  javascript lib code for RSA256 signing and SHA256 digest/hash to
the Jrsassign-js environnment variable.

It is normally there in the environment provided ING Sandbox in this repository. In case it is not, this request allowes you to download it once more and stre in the environment variable.
This script is made available through eval(Jrsassign-js). Another method to achieve the same is to put it in a collection global pre-request.
I chose this way as it made it more visual for users instead of 'hiding' it in the pre-request global section.

Other general functions I made are in envrionment variable Global JS functions.

The other request make up the functionality. I use the ING sandbox environment and the eIDAS enabled client ID and PKI pairs.
PSD2 works with eIDAS only! 

The Private keys and Certificates are stored in PrivateKeySigningPEM and eidas_signing_cert in base64 format.
The TLS keypair used for the client authentication (also of 'type' eIDAS/signed by eIDAS authority) is also in this repository.

Configure Postman to use this keypair for https://api.sandbox.ing.com in Settings > Certificates > Client Certificates.



A) Execute Request 1, 2 first. req 1 gets  you a client access token. 2, gets you the authorization server URL.
B) Open request 3, generate the curl statement by clicking on the "code" link. Copy the URL generated into your browser and execute it. 
It might take a moment for the browser to load the JS libs etc. You may want to reload the page if it stays blank.

The result is a selection window where you get to select the bank account for which you want to authorize the 3rd party to get the transactions from.

Postman is not able to run this selction screen in its Response Preview window hence the need to execute the request in the browser.

Select one and continue. The result will be an OAuth 2 authorization code being supplied in the redirect back to the redirect url example.com as parameter
This looks like: https://www.example.com/?state=761&code=06653de0-1e08-4e2f-a3af-db7e58b252c5

C) Move on to Request 4, copy and paste the authorization code  in the body of the request after the code= statement. 
Do not add a newline/carriage return at the end of the line!
Execute the request.

Final result an OAUTH 2.0 access-token that can be used in the request to the business API.

