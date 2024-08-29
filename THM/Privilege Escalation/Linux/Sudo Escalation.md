Example 1:
**What is the hash of frank's password?**  
  
When we cd back to root via cd /, and we run the id command, we can see that we do not have root access, thus we will not be able to read Frank's password. Run `cat /etc/shadow` and you will see we cannot get access.  
[![Linux PrivEsc](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2gsay6cltjbsyfops512.png)](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F2gsay6cltjbsyfops512.png)

Let's fix that. Run `sudo nano` and press CTRL+R and CTRL+X. Enter the following command to gain root access: `reset; bash 1>&0 2>&0` and press Enter.  
[![Linux PrivEsc](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F8dr3y7m7lo6p1giqby9c.png)](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F8dr3y7m7lo6p1giqby9c.png)

When we run the `id` command now, we can see that we have root access.  
[![Linux PrivEsc](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fm5rpwth1sg9tcn3h6ouh.png)](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fm5rpwth1sg9tcn3h6ouh.png)

Now we can go ahead and run `cat /etc/shadow` again and would you know it, we can now find Frank's hashed password!