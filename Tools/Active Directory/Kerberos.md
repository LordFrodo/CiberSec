https://github.com/ropnop/kerbrute/releases

use it in AD

Remember change the executable permission using "chmod u+x"


- **User enumeration**
./kerbrute_linux_amd64 userenum user.txt -d ciberseguridad.local --dc 192.168.175.143

it runs a list with possible usernames and it validate/discard depending of the result of the enumeration

- **Password Spray (Brute Force)**
./kerbrute_linux_amd64 passwordspray *'user or user -list'* *'password or password-list'* -d aulas.local --dc 172.16.0.4
