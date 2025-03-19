# Honeypot
Setting up Honeypot using Cowrie and a Raspberry Pi 5

## Ping the Pi

![image](https://github.com/user-attachments/assets/bbb0ff71-507d-41f9-aed4-a65233ea498d)

## SSH into pi@raspberrypi.local

![image](https://github.com/user-attachments/assets/a9289eae-2002-409c-bffb-21c03b6ba073)

![image](https://github.com/user-attachments/assets/c167c180-4f10-46ce-bda4-f44b729e1b00)

## Update packages

![image](https://github.com/user-attachments/assets/580aef6b-e570-4ac0-8afa-ca5de5ea6b09)

## Always read the docs https://docs.cowrie.org/en/latest/INSTALL.html

    sudo apt-get install git python3-venv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind

![image](https://github.com/user-attachments/assets/5a60a920-aa2d-4f39-8522-f83793118353)

    sudo adduser --disabled-password cowrie

![image](https://github.com/user-attachments/assets/4dccad17-950c-43a5-a82f-e1de0065935b)

    sudo su cowrie
    git clone http://github.com/cowrie/cowrie
    
![image](https://github.com/user-attachments/assets/b5ebea49-acd5-42ec-88d9-e81aeb7ce53b)

    python -m venv cowrie-env
    source cowrie-env/bin/activate
    python -m pip install --upgrade pip
    python -m pip install --upgrade -r requirements.txt
    
![image](https://github.com/user-attachments/assets/dbcf53df-8bbc-47ad-a8b4-2f961868e278)
