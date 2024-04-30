FROM debian:bookworm

ADD . /root/secbox/app/
WORKDIR /root/secbox/app
RUN apt-get update
RUN apt-get install -y nodejs yarnpkg npm

RUN npm install
ENV VUE_APP_ROOT="localhost:5000"
CMD ["npm", "run", "serve"]
