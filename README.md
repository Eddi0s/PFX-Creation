# PFX-Creation
The code is an alias command that utilizes OpenSSL to create a PFX file by combining a key, certificate, and CA bundle.

## Installation and Setup

1. Open your shell configuration file (e.g., `.bashrc`, `.zshrc`, or `.bash_profile`) using a text editor.
2. Add the following line at the end of the file to create the alias:

`alias createpfx='filename=$(ls *.crt | sed 's/\.crt$//') && (echo -e '\n\n' | openssl pkcs12 -export -out "${filename//_/.}.$(date +%Y)".pfx -inkey *.key -in *.crt -certfile $(find . -name "*.ca-bundle") -passin pass:'' -passout pass:'' ) && echo -e "\033[32mFile ${filename//_/.}.$(date +%Y).pfx has been created.\033[0m"'`

3.  Now you can execute the createpfx command in the directory of your SSL certificate.

## Functionality

The `createpfx` command performs the following steps:

##### Obtain the base filename without the .crt extension of the current CRT file to create a filename for the upcoming .pfx file generation.

`filename=$(ls *.crt | sed 's/\.crt$//')`

##### Generate two newline characters as input for the following command

`echo -e '\n\n' | `

##### Create a PFX file with the .pfx extension that includes the current year in the filename. Gather the CRT, CA bundle, and key, and leave the password field blank for the new PFX file.

`openssl pkcs12 -export -out "${filename//_/.}.$(date +%Y)".pfx -inkey *.key -in *.crt -certfile $(find . -name "*.ca-bundle") -passin pass:'' -passout pass:''`

##### Display a message indicating the successful creation of the file

`echo -e "\033[32mFile ${filename//_/.}.$(date +%Y).pfx has been created.\033[0m"`

## Required Files for Successful Code Execution

To successfully execute this code, you will need the following files:

#### Certificate Files: A file with the .crt extension in the current directory.
`Example: example.crt`

#### CA Bundle File: A file with the .ca-bundle extension in the current directory or its subdirectories.
Example: example.ca-bundle, test.ca-bundle, etc.

#### Private Key File: A file with the .key extension in the current directory.
`Example: example.key`

Ensure that these files are present in the same directory as the script or update the script to specify the correct file paths if they are located elsewhere.

## Usage

Here's an example of how to use the `createpfx` command:

Make sure you are in the directory where the SSL certificate is located.

Run the following command to execute the script:

`createpfx`

Upon successful execution, the output will be:

`File example.com.2023.pfx has been created.`



