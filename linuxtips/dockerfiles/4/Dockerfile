FROM golang AS buildando

WORKDIR /app
ADD . /app 
RUN go mod init
RUN go build -o hellogo


FROM alpine
WORKDIR /giropops
COPY --from=buildando /app/hellogo /giropops/

ENTRYPOINT ./hellogo