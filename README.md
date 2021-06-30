# hashit
Small bash script for encoding piped input to then pass on

### Install Instructions

git clone https://github.com/adamtlangley/hashit.git 
cd hashit  
chmod +x hashit  
cp hashit /usr/bin/local/

### Usage Examples

I built this little bash script with ffuf ( https://github.com/ffuf/ffuf ) usage in mind so i'll use that as my example:

Say you have an endpoint that accepts an id parameter which is a interval we could check it for IDOR using the below command which would generate a list of numbers between 1 and 1000:

`seq 1 1000 | ffuf -w - -u https://website.com/user?id=FUZZ`

This is fine but what if the id parameter accepts a hash of the integer instead such as an md5 or Base64 or Base32...
This is where hashit helps...

`seq 1 1000 | hashit md5 | ffuf -w - -u https://website.com/user?id=FUZZ`  
`seq 1 1000 | hashit b64 | ffuf -w - -u https://website.com/user?id=FUZZ`  
`seq 1 1000 | hashit b32 | ffuf -w - -u https://website.com/user?id=FUZZ`

You could even use it to check for hashes of strings instead

`cat usernames.txt | hashit md5 | ffuf -w - -u https://website.com/user?username=FUZZ` 
