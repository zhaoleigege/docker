.PHONY: build run test docker

docker:
	docker build -t mux .

test: build
	@echo "测试项目"
	go test

run: build
	@echo "运行项目"
	./buse
	
build: 
	@echo "开始编译项目"
	go build .