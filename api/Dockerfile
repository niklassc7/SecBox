FROM debian:bookworm


# Must be run with parent dir as context, see ../docker-compose.yml

ADD . /root/secbox/
WORKDIR /root/secbox/api
RUN apt-get update
RUN apt-get install -y python3 python3-pip


RUN pip install --break-system-packages -r requirements.txt

ENV DB_PORT="27017"
ENV HOST_BITNESS=64
ENV DB_HOST="mongo"
ENV DB="secbox"

CMD ["python3", "webapp_api.py"]
