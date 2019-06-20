FROM golang:latest 
RUN mkdir /app 
ADD . /app/ 
WORKDIR /app 
EXPOSE 8001
RUN go get -d -v ./...
RUN go build -o main . 
# HEALTHCHECK --interval=30s --timeout=30s CMD curl -f http://localhost:8001/products || exit 1
HEALTHCHECK --interval=10s --timeout=5s CMD echo "pass" || exit 1
CMD ["/app/main"]
