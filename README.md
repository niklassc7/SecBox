# SecBox
SecBox tool; a lightweight, container based malware analysis sandbox.
Requires Python version 3.9.

## Frontend Setup
The frontend requires [Node 16.X](https://www.stewright.me/2022/01/tutorial-install-nodejs-16-on-ubuntu-20-04/) and
 [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#debian-stable). To install the dependencies go to 
```
├── SecBox
│   ├── app
```
and run `npm install`. Create a .env file with the value VUE_APP_ROOT with the desired backend IP, e.g. `VUE_APP_ROOT="localhost:5000"` for if you are running it locally.

To start the frontend, run `npm run serve`, the frontend should now be accessible at the address you specified, e.g. `localhost:8080`.

```sh
cd app
npm install
source app.env
npm run serve
```

## Backend Setup
The backend requires [python 3.9](https://www.python.org/downloads/release/python-390/) and [pip](https://pip.pypa.io/en/stable/installation/).
All dependencies required for the backend can be installed in
```
├── SecBox
│   ├── api
```
with `pip install -r requirements.txt`.

Also recommended `python-gevent-websocket`.

Setup a [mongo DB](https://www.mongodb.com/) database.
```sh
# Arch
yay -S mongodb-bin
sudo -u mongodb /usr/bin/mongod --config /etc/mongodb.conf

# Ubuntu 22.04
sudo apt-get install gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl daemon-reload
sudo systemctl start mongod


# Check DBs
# The DB will be created automatically by SecBox if the mongodb-daemon is running
# and `webapp_api.py` is started.
mongosh
show dbs
```


Create an .env file in this directory:
```sh
export DB_PORT="27017"
export HOST_BITNESS=64
export HOST="mongodb+srv://"
export DB= "DB?"
```

So for a local database called "secbox" this could look like

```sh
export DB_PORT="27017"
export HOST_BITNESS=64
export HOST="localhost"
export DB="secbox"
```

Finally run:
```sh
cd api
[ -d .venv ] || python3 -m venv .venv
# Replace api.env with your env-file
source .venv/bin/activate
pip install -r requirements.txt
source api.env
python3 webapp_api.py
```

## Host Setup
```
├── SecBox
│   ├── host
```

In order to set up the host on a machine, run:

```sh
# If an up-to-date docker is available in your distribution skip setup.sh
sudo ./setup.sh
./setup_bazel_gvisor.sh
```

The host can then be run from the host directory by running:

```sh
cd host
sudo -s
[ -d .venv ] || python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
source host.env
python3 host.py
```


## Configuration
Configuration happens through the respective .env files for the respective system components.


## Demo Video
A demo is available on YouTube:
https://www.youtube.com/watch?v=lkEE3iQvFtk
