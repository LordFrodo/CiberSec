Hydra supports many protocols, including FTP, POP3, IMAP, SMTP, SSH, and all methods related to HTTP. The general command-line syntax is: `hydra -l username -P wordlist.txt server service` where we specify the following options:

- `-l username`: `-l` should precede the `username`, i.e. the login name of the target.
- `-P wordlist.txt`: `-P` precedes the `wordlist.txt` file, which is a text file containing the list of passwords you want to try with the provided username.
- `server` is the hostname or IP address of the target server.
- `service` indicates the service which you are trying to launch the dictionary attack.

Consider the following concrete examples:

- `hydra -l mark -P /usr/share/wordlists/rockyou.txt 10.10.32.93 ftp` will use `mark` as the username as it iterates over the provided passwords against the FTP server.
- `hydra -l mark -P /usr/share/wordlists/rockyou.txt ftp://10.10.32.93` is identical to the previous example. `10.10.32.93 ftp` is the same as `ftp://10.10.32.93`.
- `hydra -l frank -P /usr/share/wordlists/rockyou.txt 10.10.32.93 ssh` will use `frank` as the user name as it tries to login via SSH using the different passwords.

There are some extra optional arguments that you can add:

- `-s PORT` to specify a non-default port for the service in question.
- `-V` or `-vV`, for verbose, makes Hydra show the username and password combinations that are being tried. This verbosity is very convenient to see the progress, especially if you are still not confident of your command-line syntax.
- `-t n` where n is the number of parallel connections to the target. `-t 16` will create 16 threads used to connect to the target.
- `-d`, for debugging, to get more detailed information about what’s going on. The debugging output can save you much frustration; for instance, if Hydra tries to connect to a closed port and timing out, `-d` will reveal this right away.


TO CONNECT TO SPECIFIC PORT AND SERVICE
`hydra -vv -l quinn -P /usr/share/wordlists/rockyou.txt.gz ftp://10.10.84.98:10021`
