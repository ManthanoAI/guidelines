   FROM continuumio/anaconda3:latest

   COPY requirements.txt /tmp/

   RUN cat /tmp/requirements.txt | xargs -n 1 pip install