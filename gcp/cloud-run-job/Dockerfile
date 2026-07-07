FROM google/cloud-sdk

RUN apt-get install -y python3-venv
ENV VENV=/opt/venv
RUN python3 -m venv $VENV
ENV PATH="$VENV/bin:$PATH"

WORKDIR /arp
COPY ./app/requirements.txt .
RUN python3 -m pip install -r requirements.txt --require-hashes --no-deps

COPY app ./app                              # bake the application in (no GCS pull at runtime)
COPY gcp/cloud-run-job/main.sh ./main.sh
COPY gcp/settings.ini ./settings.ini
RUN chmod +x ./main.sh ./app/run-local.sh

ENTRYPOINT ["./main.sh"]
