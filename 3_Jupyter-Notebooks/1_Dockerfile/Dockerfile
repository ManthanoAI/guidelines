   FROM continuumio/anaconda3:latest

   COPY requirements.txt /tmp/

   RUN /opt/conda/bin/python -m pip install --upgrade pip

   RUN cat /tmp/requirements.txt | xargs -n 1 pip install