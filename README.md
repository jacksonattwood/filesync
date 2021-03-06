# filesync
 
 A script to sync multiple servers with a central listening server, that provides them all with authenticated access to folders on the central server. 

 This script was originally designed to sync SSL Certificates with multiple servers, but now has a much more generic purpose. 
 
 <!-- A script to sync multiple servers with a central listening server, that provides them all with the same SSL certificate (for ease of use)
 This can be used to sync any files you want, just set the folders and filenames to whatever you'd prefer
 Since this just uses some basic GET requests, you can easily integrate with any  -->

# Installation

## Server
1. Clone into the repo: `git clone https://github.com/jacksonattwood/filesync.git && cd filesync`
2. Run the following command on your CLI to install all the required modules: `npm install`
3. Copy "config.json.example" to "config.json" and edit to your needs (DO NOT SHARE YOUR AUTH KEY WITH ANYONE)
4. Run the following command on your CLI to start the NodeJS Server: `node server.js`

## Client
1. Download the code
    - ## In your web browser: 
        - Visit the site hosted by your Node.JS script (e.g. `https://syncserver.jcksn.rip:7080/`)
        - Extract the ZIP downloaded
        - Configure the Python script as required (server, download location, auth key etc.)
    - ## From CLI:
        - Use cUrl or Wget to download the hosted zip: `curl -X GET http://server:port -o client.zip`
        - Extract the folder however you wish
        - `cd` into the folder

    - You can also just download from GitHub if you want
2. Copy `config.py.example` to `config.py` and make your desired changes
3. Run `client.py`

# Configuration options
## Server
- `port`: The port you would like the server to listen on (default: `7080`)
- `https`: Enable or disable HTTPS + SSL authentication (`true` or `false`, default enabled)
    - `certificate`: Path to SSL certificate (cert.pem, cert.crt etc.)
    - `privatekey`: Path to SSL private key (priv.key etc.)
- `authkey`: The authorisation key you would like to use for your client script
- `autherror`: The message to return when a request fails authentication
- `logging`: Whether you would like to log access requests to console and to an `access.log` file (1: YES, 2: NO)
- `client_download_enabled`: whether you would like to be able to get the zip from the server when not using an access key (1: YES, 2: NO)
- `certroot`: The directory above all the files  you are trying to download

# Testing
In your CLI run: 
## HTTP
- `curl -X GET http://127.0.0.1:7080 -H "auth-key: yourauthkey" -H "file: /test.crt"` 
## HTTPS
- `curl -k -X GET https://127.0.0.1:7080 -H "auth-key: yourauthkey" -H "file: /test.crt"`

and make sure to replace server address, port, auth-key and file location to one that exists on your server

# Things to do:
- [x] Add HTTPS support (will be optional, but preferred)
- [x] Add optional access logging
- [ ] Automatically set server address in client configuration