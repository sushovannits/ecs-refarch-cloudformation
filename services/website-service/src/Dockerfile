FROM golang:latest 
RUN mkdir /app 
ADD . /app/ 
WORKDIR /app 
EXPOSE 8000
RUN go get -d -v ./...
RUN go build -o main . 
HEALTHCHECK --interval=30s --timeout=30s CMD curl -f http://localhost:8000/ || exit 1
CMD ["/app/main"]
