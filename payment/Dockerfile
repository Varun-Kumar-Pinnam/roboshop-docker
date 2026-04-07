FROM python:3.9.25-alpine3.22 AS builder
WORKDIR /app
RUN apk add --no-cache build-base linux-headers pcre-dev
COPY requirements.txt .
#--prefix=/install, to create the compile code in /install folder, otherwise it create at OS level in default folder.
RUN pip3 install --prefix=/install -r requirements.txt



FROM python:3.9.25-alpine3.22
EXPOSE 8080
WORKDIR /app
RUN apk add --no-cache pcre
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /app
COPY --from=builder /install /usr/local
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt .
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]




# FROM python:3.9
# EXPOSE 8080
# WORKDIR /app
# COPY *.py .
# COPY payment.ini .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi","--ini","payment.ini"]

