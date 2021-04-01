TEST?=$$(go list ./... | grep -v 'vendor')

HOSTNAME=hashicorp.com
NAMESPACE=kestra-io
NAME=kestra
BINARY=terraform-provider-${NAME}
VERSION=0.1
OS_ARCH=linux_amd64

default: install

build:
	go build -o ${BINARY}


doc:
	go generate

install: build
	mkdir -p ~/.terraform.d/plugins/${HOSTNAME}/${NAMESPACE}/${NAME}/${VERSION}/${OS_ARCH}
	mv ${BINARY} ~/.terraform.d/plugins/${HOSTNAME}/${NAMESPACE}/${NAME}/${VERSION}/${OS_ARCH}

test:
	go test -i $(TEST) || exit 1
	echo $(TEST) | xargs -t -n4 go test $(TESTARGS) -timeout=30s -parallel=4

testacc:
	TF_ACC=1 go test $(TEST) -v $(TESTARGS) -timeout 120m
