# SAML Parser
A simple Java command-line utility to decrypt `EncryptedAssertion` objects in OpenSAML data.

## Requirements
 * Java
 * Maven

## Installation

```
mvn clean install
```

This will build the utility and download any dependencies that might be required.
A `target` folder will be created that has (among others) a JAR file with the suffix `jar-with-dependencies.jar`.
This is the command line utility.

## Usage

```
$ java -jar target/org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar -h
Usage:
java -jar org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar idpPublicKey spPublicKey spPrivateKey inputData inputEncoding outputEncoding

Parameters
 * idpPublicKey
    This is the Identity Provider's public key that can be used to verify signatures in SAML data.
 * spPublicKey
    This is your Service Provider's public key that the IdP uses to encrypt SAML data.
 * spPrivateKey
    This is your Service Provider's public key that can be used to decrypt SAML data.
 * inputData
    The SAML data that needs decrypting (if any.)
 * inputEncoding
    The encoding format that the inputData is passed in.
    Currently only supports 'base64' or 'plain', defaults to 'plain'.
 * outputEncoding
    The encoding format that the decrypted data should be outputted in.
    Currently only supports 'base64' or 'plain', defaults to 'plain'.

Examples:
    java -jar org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar <idpPublicKey> <spPublicKey> <spPrivateKey> '<XML data>'
    java -jar org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar <idpPublicKey> <spPublicKey> <spPrivateKey> '<base64-encoded XML data>' 'base64'
    java -jar org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar <idpPublicKey> <spPublicKey> <spPrivateKey> '<base64-encoded XML data>' 'base64' 'base64'
```
```
It seems that loading xml data in as plain has problems parsing xml properly, encoding it as base64 seems to resolve the issue
suggested usage for ease of use assuming windows powershell but unix systems will be similar
$key = cat ./privatekey.pem
$pub = cat ./pubkey.pem
$assertion = cat ./assertion.txt

at present this has the idppublickey signature verification disabled non gracefully, but requires a valid cert in it's place
java -jar org.sakaiproject.Hilary.SAMLParser-1.0-SNAPSHOT-jar-with-dependencies.jar $pub $pub $key $assertion 'base64'

pem file cert input must not have carriage returns or line breaks included in the file, my test also removed the begin cert/end cert characters, but have not verified if it works with that included.
```
## License

```
Copyright 2013 Apereo Foundation (AF) Licensed under the
Educational Community License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may
obtain a copy of the License at
 
      http://www.osedu.org/licenses/ECL-2.0
 
 Unless required by applicable law or agreed to in writing,
 software distributed under the License is distributed on an "AS IS"
 BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express
 or implied. See the License for the specific language governing
 permissions and limitations under the License.
```
