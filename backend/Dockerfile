FROM python:3.8-slim

WORKDIR /app

COPY . .

RUN chmod +x start-backend.sh

RUN sed -i 's/\r$//' start-backend.sh

RUN pip install --upgrade pip
RUN pip install -r requirements.txt

ENV FLASK_APP=run.py
EXPOSE 5000

ENTRYPOINT ["./start-backend.sh"]

