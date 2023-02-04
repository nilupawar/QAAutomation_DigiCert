# QAAutomation_DigiCert

* ## When certificate is imported from Browser
    - If you save as 'DER' file then it saves as binary
    - If you save as 'BASE64' encoded then we get cert which has --BEGIN CERT and ---END CERT line in it. (Usually .pem file has this content)


<br>

* ## Certificate file extension
    - .pem -> This is base64 encoded file (it can contain certificate and private key)
    - .p12 -> It is basically a keystore, it saves key and certificate
    <br><br>
    you can create .p12( keystore ) if you have cert(base64 encoded) and key ( usually both are in .pem file)
    <br><br>
    command to create .p12( keystore) 
        
          openssl pkcs12 -export -inkey <keyfile> in <cetificatefile> -out <keystorename>.p12

          note : If this commands get stuck then add 'winpty' at the begining of the command       

<br>

* ## Convert der or binary certificate to a BASE64/PEM format certificate

        Openssl x509 -inform der -in <source_file> -out <dest_file.pem/cer>
<br>

* ## If you want get the certificate chain of a portal run below openssl command


        openssl s_client -showcerts -connect <hostname>:443 < /dev/null

        E.g. openssl s_client -showcerts -connect youtube.com:443 < /dev/null

        NOTE: I have noticed that when used the above command for 'github.com' it did not print the root CA cert details.
<br>

* ### Tip 

        - If you want to override the 'cacerts' (jdk truststore) then you can keep your certs in truststore file 'jssecacerts'. jdk will read it first.

        This approach can also be followed when you don't want to loose you trust store when jdk is updated

        - You can access/print clip board content in gitbash by 'cat /dev/clipboard' command. 

        - If you want to base64 decode a string copied to your clip board and if the plain text contains non-aplabetic charater also then use below command 
            * cat /dev/clipboard | base64 -di    (i is used to ignore non-alphabet characters)   

        - System property to provide truststore and keystore details are as follow
            * javax.net.ssl.truststore
            * javax.net.ssl.truststore.password  
            * javax.net.ssl.keyStore
            * javax.net.ssl.keyStorePassword
            * javax.net.ssl.keyStoreType
            * javax.net.ssl.trustStoreType

        - Default keystore type as prescribed in java.security file has been changed to pkcs12 from jks from Java 9 onwards.

        - 