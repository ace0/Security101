# Security101
A list of the basic computer security items that should be considered when putting a product or service into production or connecting it or any computer to the internet.

### About
This list was inspired by the following blog post: http://newschoolsecurity.com/2015/01/security-101-show-your-list/

### Contribute
Please send candidate updates to this list via email to ace@cs.wisc.edu or by submitting a pull request.

# The List

## Web sites and web services on the internet

### Store and validate passwords using bcrypt, scrypt, or PBKDF2.
No plaintext passwords, no simple hashing, not even simple hashing with salts.

### Use TLS (also called HTTPS) to send and receive sensitive information from clients
Sensitive information includes: usernames, passwords, PINs, and financial information (like bank account numbers, credit and debit card numbers). Even better, use TLS for everything: servers are fast, the overhead isn't too bad, and it's a much simpler policy.

### Sanitize inputs used for database queries
Avoid SQL injections by assuming client-provided inputs (including hidden form elements or cookies) are malicious. All production-quality database interface 

### Use SSH with public key authentication to administer remote servers
Whenever possible, public-key authentication is typically more secure than username/password authentication and relatively easy to setup. Once configured on the remote server and the local workstation or laptop, logins to remote servers are even easier than using passwords. 

Never use unencrypted channels to administer remote servers: no telnet, unencrypted FTP. SSH is ubiquitious and easy to use.

## Cryptography
### Hash Functions
Use current, NIST-approved standards: SHA2, SHA3. No broken or deprecated hash functions like MD5 or SHA1.
