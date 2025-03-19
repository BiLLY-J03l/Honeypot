# Honeypot
Setting up Honeypot using Cowrie and a Raspberry Pi 5

## Ping the Pi

![image](https://github.com/user-attachments/assets/bbb0ff71-507d-41f9-aed4-a65233ea498d)

## SSH into your PI

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

    cd ~/cowrie/etc
    cp cowrie.cfg.dist cowrie.cfg
    nano cowrie.cfg

![image](https://github.com/user-attachments/assets/b5b14a5f-3797-4724-91e3-6a78c9a990c8)
![image](https://github.com/user-attachments/assets/9e61c68a-6d90-486b-8080-57ba226dab42)

    iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
    iptables -t nat -A PREROUTING -p tcp --dport 23 -j REDIRECT --to-port 2223
![image](https://github.com/user-attachments/assets/68cbebfa-d2f0-4b55-828c-2ff2a29bb8b9)


## Start the honeypot

    bin/cowrie start
    
![image](https://github.com/user-attachments/assets/ab2ce8a9-1fd2-44aa-b4b9-439eb2619ca8)

- check if it's running in the background

      ps aux | grep cowrie

![image](https://github.com/user-attachments/assets/bd8b4dd4-d2f0-410f-ae76-1a73471cb156)


## Now, Monitor any suspicious actions

    tail -f ~/cowrie/var/log/cowrie/cowrie.log
    
![image](https://github.com/user-attachments/assets/94623411-a619-4c00-a7c3-85ecfb6850c8)


## TESTING

- I ran an nmap scan on the ports and it was logged by the honeypot

    ![image](https://github.com/user-attachments/assets/8daa8076-0a55-4782-b961-550af632e875)
    ![image](https://github.com/user-attachments/assets/31823a7c-ad63-4374-99bf-7a3bfb8d34be)

- Then I used NSE to brute-force my way into the ssh port
    ![image](https://github.com/user-attachments/assets/827f4ef8-6a3b-44db-ab28-d48c401b7884)
    ![image](https://github.com/user-attachments/assets/52470edf-d8ec-4383-bd08-8d64a30854a8)

- And all the attempts were logged in the cowrie.log file
    ![image](https://github.com/user-attachments/assets/6303bb3d-af8e-4bb2-ab63-8ef358164a67)

- Now, I will login as the adversary from my Ubuntu machine.
    ![image](https://github.com/user-attachments/assets/53bbdd41-7951-452b-b16b-7cb9d35119bf)
    ![image](https://github.com/user-attachments/assets/d04dc1e4-9196-4944-8aad-485af287a4ac)
    ![image](https://github.com/user-attachments/assets/f80821d3-6a04-4139-8a14-e0418a71d865)
    ![image](https://github.com/user-attachments/assets/4452ce7b-13ab-4d1e-90ef-971d568a0903)


## Analysis

- On the honeypot, you can navigate to ~/cowrie/var/lib/cowrie/tty and use ~/cowrie/bin/playlog [tty_file] to replay the session with which the attacker was interacting with.
![image](https://github.com/user-attachments/assets/bfd09817-85b8-4400-a2f0-21467456188d)

- How this could benefit us?
    - the adversary might replace the ssh key to take over the server or type in his FTP credentials in the process of exfiltrating "sensitive" data.
    - Congratulations, now you can sit back, relax, watch a child play around and hack the hacker.
 
## (Optional) Setting up ELK stack to visulaize the logs -> https://docs.cowrie.org/en/latest/elk/README.html

    wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
    apt-get update

![image](https://github.com/user-attachments/assets/a6d8395b-adeb-4203-9579-d14bef9d93c8)

    sudo apt -y install apt-transport-https wget default-jre
    sudo apt install elasticsearch logstash kibana
    sudo apt install filebeat
    sudo apt install nginx apache2-utils

![image](https://github.com/user-attachments/assets/5da76610-78d1-4cde-b0e2-d0f1de70a6e2)

    sudo systemctl enable elasticsearch logstash kibana filebeat nginx


## Configuration

### ElasticSearch Configuration

### Kibana Configuration

### Logstash Configuration

### FileBeat Configuration

### Nginx Configuration






