sudo apt install libssl-dev libffi-dev python3-dev build-essential
sudo apt update
sudo apt install python3-pip
pip3 install requests
sudo apt install python3-pip
python3 k7.00.py
--------------------------------------------------------------
sudo apt update
sudo apt install build-essential libssl-dev libffi-dev python3-dev

sudo apt --fix-broken install

sudo apt install --reinstall python3-apt

sudo apt update
sudo apt upgrade
==================================================
wget https://files.pythonhosted.org/packages/6b/47/8e0dbaafc92f34b34e3c75b6a2a4f5c735f4c5debf28fe2d6c1f25f09b9c/requests-2.31.0.tar.gz

tar -xvzf requests-2.31.0.tar.gz
cd requests-2.31.0

python3 setup.py install --user

import requests
