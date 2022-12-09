# Subdomain-Enumeration-


jasarth12@gmail.com
Write a Bash script that is used to perform subdomain enumeration. The script uses various tools to find subdomains of a given domain, such as Findomain, SubFinder, Amass, and AssetFinder.

Here is an example Bash script for subdomain enumeration:

Copy code
#!/bin/bash

# Define the domain for which to enumerate subdomains
domain="example.com"

# Install the tools if they are not already present on the system
if ! [ -x "$(command -v findomain)" ]; then
  echo "Installing Findomain..."
  sudo apt-get install findomain
fi
if ! [ -x "$(command -v subfinder)" ]; then
  echo "Installing Subfinder..."
  go get -u github.com/subfinder/subfinder
fi
if ! [ -x "$(command -v amass)" ]; then
  echo "Installing Amass..."
  go get -u github.com/OWASP/Amass/...
fi
if ! [ -x "$(command -v assetfinder)" ]; then
  echo "Installing Assetfinder..."
  go get -u github.com/tomnomnom/assetfinder
fi

# Use Findomain to find subdomains
echo "Running Findomain..."
findomain -t $domain > findomain-results.txt

# Use SubFinder to find subdomains
echo "Running Subfinder..."
subfinder -d $domain > subfinder-results.txt

# Use Amass to find subdomains
echo "Running Amass..."
amass enum -d $domain > amass-results.txt

# Use AssetFinder to find subdomains
echo "Running Assetfinder..."
assetfinder --subs-only $domain > assetfinder-results.txt

# Combine the results from all tools into a single file
echo "Combining results..."
cat findomain-results.txt subfinder-results.txt amass-results.txt assetfinder-results.txt | sort -u > all-results.txt

echo "Subdomain enumeration complete. Results saved in all-results.txt."
This script performs the following steps:

Defines the domain for which to enumerate subdomains.
Installs the required tools (Findomain, SubFinder, Amass, and AssetFinder) if they are not already present on the system.
Uses each of the tools to find subdomains of the given domain, and saves the results to a separate file.
Combines the results from all tools into a single file, sorts the results to remove duplicates, and saves the final list of subdomains.
Note: This script assumes that the apt-get and go commands are available on the system. It also assumes that the user has the necessary permissions to install the required tools.
