# Python

## set python 3 as default

The last number is the priority. Greater number is higher priority. 

```shell
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 1
 
```

If you want to check the current config run `sudo update-alternatives --config python`

## install pip for python3

```shell
sudo apt install python3-pip
```