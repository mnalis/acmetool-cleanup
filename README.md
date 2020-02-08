# acmetool-cleanup
cleanup for https://hlandau.github.io/acmetool/

Using `acmetool want xxxx` to create certificates with SubjectAltNames might create multiple certificates 
which get keep getting renewed all the time. This can lead to hitting Let's Encrypt limits.

for example you may request single certificate which contains entries for `a.example.com` and `b.example.com` 
by using `acmetool want a.example.com b.example.com`.

When you later want to add extra domain and run `acmetool want a.example.com b.example.com c.example.com` it will
request new certificate, but old one will still remain and will keep getting renewed.

You can check if this is happening to you by looking at Certificate Transparency Logs - https://crt.sh/

This tool tries to find such superceded certificates and print instructions for their removal.
