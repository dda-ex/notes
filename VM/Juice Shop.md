# Creating Juice Shop

Create VM OWASP Juice Shop

Update the system
```bash
curl -L https://deb.nodesource.com/setup_19.x -o nodesource_setup.sh
```

Execute the script
```bash
chmod +x nodesource_setup.sh
sudo ./nodesource_setup.sh
```

Install nodejs
```bash
sudo apt-get install nodejs git -y
```

Download juice shop source file or download the last relase check in github [[Git]]]
```bash
git clone https://github.com/juice-shop/juice-shop.git --depth 1
```

Edit the crontab to autostart the service
```bash
sudo crontab -e
sudo npm start --prefix /home/juice/juice-shop/ | xclip -i
```

Edit `/etc/issue`
```bash
juice-shop web app: http://\4:3000
```
