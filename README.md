# Security 101
A list of the basic computer security items that should be considered when putting a product or service into production or connecting a device to the internet.

#### About
This list was inspired by the following blog post: http://newschoolsecurity.com/2015/01/security-101-show-your-list/

#### Contribute
Please send candidate updates to this list via email to ace@cs.wisc.edu or by submitting a pull request.

# The List

## Production Services on the Internet

#### Store and validate passwords using bcrypt, scrypt, or PBKDF2.
No plaintext passwords, no simple hashing, not even simple hashing with salts.

#### Use TLS (also called HTTPS) to send and receive sensitive information from clients
Sensitive information includes: usernames, passwords, PINs, and financial information (like bank account numbers, credit and debit card numbers). Even better, use TLS for everything: servers are fast, the overhead isn't too bad, and it's a much simpler policy.

#### Sanitize inputs used for database queries
Avoid SQL injections by assuming client-provided inputs (including hidden form elements or cookies) are malicious. All production-quality database libraries have techniques to sanitize untrusted inputs and generate queries that resist SQL injection. Use these.

#### Use SSH with public key authentication to administer remote servers
Whenever possible, public-key authentication is typically more secure than username/password authentication and relatively easy to setup. Once configured on the remote server and the local workstation or laptop, logins to remote servers are even easier than using passwords. 

Never use unencrypted channels to administer remote servers: no telnet, unencrypted FTP. SSH is ubiquitious and easy to use.

---
## Cryptography

### No homebrew cryptography in production systems
Hoembrew algorithms and implementations are fine for security researchers and hobbyists. It's how we learn! But production systems need tried-and-true algorithms and trusted implementations. Current implementations are often still flawed, unfortunately (see TLS Heartbleed), but homebrew is often even worse. Unless you understand why things like semantic security and constant-time algorihtms are important, you probably shouldn't be designing, implementing, and putting cryptography into production.

#### Get random numbers from a secure source
If you need ranodm numbers for security, your operating system and crypto library (like OpenSSL) have secure random numbers. Your programming language probably even has a wrapper for reading the OS-provided random number generat (RNG). Don't try running the time-of-day and your favorite Spice Girl through MD5 to generate secure random numbers.

#### Use AES and authenticated encryption for symmetric cryptography
AES is the current NIST-approved standard for symmetric cryptography. Authenticated encryption with associated data (AEAD) modes like Gallois Counter Mode (GCM) provide encrytion and authentication in a single primitive. Ensuring both encryption and authentication is critical and getting it right can be tricky. (In some cases, Mac-then-encrypt can be insecure.) Using an AEAD mode simplifies things and improves the chances of getting it right.

#### Use SHA2 and SHA3 for hashing
SHA2 (also called SAH-256, SHA-512) and SHA3 are the current NIST-approved secure hash functions. Don't use broken or deprecated hash functions like MD5 or SHA1 for security-sensitive operations.
