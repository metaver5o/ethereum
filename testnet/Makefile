NAME:= m4rc0/eth-node
CI_REGISTRY:= docker.io
TIMESTAMP:= `date +%Y`-`date +%m`-`date +%d`-`date +%s`
BRANCH:= $$(`git branch|awk {'print $$2'}`)
REVISION:= $$(git rev-parse HEAD)
USER:= $$(git config user.name)
VERSION:= latest
CONTAINER_NAME:= eth-node

.PHONY: all build run test release dockerfile kill 

all: build run exec

build:
	docker build -t $(NAME):$(VERSION) --rm .

run:
	@echo 'running ${CONTAINER_NAME}'
	docker run -dit --name ${CONTAINER_NAME} -v $(PWD)/root/:/root/ -p8545:8545 ${NAME} 

exec:
	docker exec -w /home/eth_user -ti ${CONTAINER_NAME} "/usr/bin/geth --rpc --rpcaddr="0.0.0.0" --testnet --cache=512 console"

# release: 
#   	docker login -u ${CI_REGISTRY_USER} -p ${CI_REGISTRY_PASSWORD} ${CI_REGISTRY}
# 	docker push $(NAME):$(VERSION)

kill:
	docker stop $(CONTAINER_NAME)
	docker rm -f $(CONTAINER_NAME)

logs:
	docker logs $(CONTAINER_NAME) -f

shell:
	docker exec -ti --user root $(CONTAINER_NAME) bash

restart:
	docker restart $(CONTAINER_NAME)