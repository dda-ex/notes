# Creating Juice Shop

## Create VM OWASP Juice Shop
Download the nodejs specific version 
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

There are two options to build Juice Shop Application, first from source code and from official releases.

## From source
Download juice shop source file or download the last relase check in github [[Git]]]
```bash
git clone https://github.com/juice-shop/juice-shop.git --depth 1
```

## From lastest release
Download the lastest release for Juice Shop from here https://github.com/juice-shop/juice-shop/releases/

## Continue with JS configuration
Edit the crontab to autostart the service
```bash
sudo crontab -e
sudo npm start --prefix /home/juice/juice-shop/ | xclip -i
```

Edit `/etc/issue`
```bash
juice-shop web app: http://\4:3000
```
