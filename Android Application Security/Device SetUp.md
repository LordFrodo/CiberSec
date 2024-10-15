https://dev.to/janetmutua/installing-android-studio-on-ubuntu-2204-complete-guide-1kh8


![[Pasted image 20241010194043.png]]
![[Pasted image 20241010194958.png]]

Clone RootAVD from gitlab in the folder tools and download the APk from the latest Magisk at Github, copy the Magisk file downloaded and save it like this "Magisk.zip".

Run "rootAVD" at tools folder
Run ".rootAVD.sh"
Search your current platform and run the commands
The last one command search your current API and copy the command until "./rootAVD.sh system-images/android-31/google_apis_playstore/x86_64/ramdisk.img"


Set up BurpSuite Certificate

Make a new folder and keep it empty.
Enter to the folder and run the following commands:

openssl req -x509 -days 365 -nodes -newkey rsa:2048 -outform der -keyout priv.key -out certificate.der -extensions v3_ca

openssl x509 -inform DER -outform PEM -text -in certificate.der -out certificate.pem

openssl rsa -in priv.key -inform pem -out priv.key.der -outform der

openssl pkcs8 -topk8 -in priv.key.der -inform der -out priv.key.pkcs8.der -outform der –nocrypt


OPCIONAL

 openssl pkcs12 -inkey priv.key -in certificate.pem -export -out certificate_full.p12

Now, open BurpSuite, go to Proxy settings and import your new Certificate (preferred the full.p12). When the import was successfully, edit your proxy listener to listen all the interfaces and at the "Request Handling" vies, check the support invisible proxying.

Now open your search browser at your phone and search your main device IP at the port 8080 and download the burpsuite certificate. Go to settings "CA Certificates" and install your certificate. Check was successfully instales at "Trusted Credentials" at the "User" view.

![[Pasted image 20241008153741.png]]