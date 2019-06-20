all: run

# This makefile contains some convenience commands for deploying and publishing.

# For example, to build and run the docker container locally, just run:
# $ make

# or to publish the :latest version to the specified registry as :1.0.0, run:
# $ make publish version=1.0.0

name = bacchus-ecs-spike-test-product-service
registry = 943289235861.dkr.ecr.ap-southeast-2.amazonaws.com
version ?= latest

binary:
	$(call blue, "Building Linux binary ready for containerisation...")
	docker run --rm -it -v "${GOPATH}":/gopath -v "$(CURDIR)":/app -e "GOPATH=/gopath" -w /app golang:latest sh -c 'go get -d -v ./...; go install -v ./...; CGO_ENABLED=0 go build -a --installsuffix cgo --ldflags="-s" -o app'

image: 
	$(call blue, "Building docker image...")
	docker build -t ${name}:${version} .
	$(MAKE) clean

run: image
	$(call blue, "Running Docker image locally...")
	docker run -i -t --rm -p 8001:8001 ${name}:${version} 

publish:  
	$(call blue, "Publishing Docker image to registry...")
	docker tag ${name}:latest ${registry}/${name}:${version}
	docker push ${registry}/${name}:${version} 

clean: 
	@rm -f app 

define blue
	@tput setaf 6
	@echo $1
	@tput sgr0
endef
