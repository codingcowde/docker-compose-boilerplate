# Boilerplate for docker-compose project with nginx and certbot

Use this boilerplate code to serve your web app with nginx and certbot


## How to setup? 

1. Open the docker-compose.yml and add your services
2. Open the file install_cert_bot.sh and rename the example.com to your actual domain name
3. Run chmod +x install_cert_bot.sh and make sure it is executable
    ```bash
    $ chmod +x install_cert_bot.sh
    ```
4. Run chmod +x renew_cert_bot.sh to make sure this is ready when needed
    ```bash
    $ chmod +x install_cert_bot.sh
    ```
5. Go to the folder nginx and rename the before-certificate-default.conf to default.conf
    ```bash
    $ cd nginx
    $ mv before-certificate-default.conf default.conf
    ```
6. Open the default.conf and change the api in upstream to your service name and example.com for your domain
7. Go back to the project root and run docker-compose up --build -d
    ```bash
    $ docker-compose up --build -d
    ```
8. After everything was built and you are back in control of your terminal, run the install_cert_bot.sh
    ```bash
    $ ./install_cert_bot.sh
    ```
9. Now go again to the nginx folder. Remove the default.conf and rename the after-certificate-default.conf to default.conf
      ```bash
    $ cd nginx
    $ rm default.conf
    $ mv before-certificate-default.conf default.conf
    ```
10. Open the default.conf and change the api in upstream to your service name and example.com for your domain


After starting your docker-compose project again, your app should now be served by nginx using the certificate obtained by certbot.

## How to renew? 

Your certificate is due for renewal every 3 month. It is recommended to renew the certificate 3 weeks before it is due. 

You can do this manually just running the renew_cert_bot.sh script
```bash
./renew_cert_bot.sh
```

Or you can set up a schedule task with your prefered task scheduler. Here is an example for a certificate obtained on the 1. January and a task set in cron to renew every 2 month on the first:

```cron
* * 1 */2 * /path/to/your/project/renew_cert_bot.sh
```

