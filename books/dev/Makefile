export PROJECT = m102
# ....
export DB_USER = usermaster
export DB_PASSWORD = passmaster
export DB_ADMIN_USER = adminmaster
export DB_ADMIN_PASSWORD = passmaster

# target:
# target: all - Default target. Does nothing
.PHONY: all
all:
	@echo "Hello $(LOGNAME), nothing to do by default"


# target: help - Display callable targets
.PHONY: help
help:
	@egrep "^# target:|-\ .+" [Mm]akefile --color=auto|column -t -s -



# target:
# target: ===== pull ======== - ============================

# target: pull_mongo - pull mongodb images
.PHONY: pull_mongo
pull_mongo:
	@echo "---> pull mongo:3.5"
	@docker pull mongo:3.5



# target: pull_all - pull base images
.PHONY: pull_all
pull_all:
	@make pull_mongo
	@make pull_python


# target:
# target: ===== build ======= - ============================

# target: build_storage - build storage image
.PHONY: build_storage
build_storage:
	@echo "---> build storage"
	@docker-compose \
		-p $(PROJECT) \
		-f build.yml \
		build storage


# target: build_all - build all images
.PHONY: build_all
build_all:
	@make build_storage


# target:
# target: ===== bootstrap === - ============================

# target: bootstrap_storage - bootstrap storage contaner
.PHONY: bootstrap_storage
bootstrap_storage:
	@echo "---> bootstrap storage"	
	@docker-compose \
		-p $(PROJECT) \
		-f bootstrap.yml \
		run \
		--rm \
		storage



# target: bootstrap_all - bootstrap all images
.PHONY: bootstrap_all
bootstrap_all:
	@make bootstrap_storage

# target:
# target: ===== shell ======= - ============================

# target: shell_mongoshell - shell mongoshell container
.PHONY: shell_mongoshell
shell_mongoshell:
	@docker-compose \
		-p $(PROJECT) \
		-f run.yml \
		run \
		--rm \
		--name $(PROJECT)_mongoshell_1 \
		mongoshell

# target: shell_mongoshell2 - shell mongoshell container
.PHONY: shell_mongoshell2
shell_mongoshell2:
	@docker-compose \
		-p $(PROJECT) \
		-f run.yml \
		run \
		--rm \
		--name $(PROJECT)_mongoshell_2 \
		mongoshell2

# target: shell_mongoshell3 - shell mongoshell container
.PHONY: shell_mongoshell3
shell_mongoshell3:
	@docker-compose \
		-p $(PROJECT) \
		-f run.yml \
		run \
		--rm \
		--name $(PROJECT)_mongoshell_3 \
		mongoshell3		



# target:
# target: ===== misc ======== - ============================

# target: down - shutdown all contaner in project
.PHONY: down
down:
	@docker-compose \
		-p $(PROJECT) \
		-f run.yml \
		down	


# target: ps - watch all process all contaner in project
.PHONY: ps
ps:
	@docker-compose \
		-p $(PROJECT) \
		-f run.yml \
		ps

# target: clear - clear untuged images in project
.PHONY: clear
clear:
	@../../scripts/clear_untagged.sh


# target: images - show all images in project
.PHONY: images
images:
	@docker images |grep $(PROJECT)


# target: volumes - show all volumes in project
.PHONY: volumes
volumes:
	@docker volume ls |grep $(PROJECT)


# target: rmi - remove all images in project
.PHONY: rmi
rmi:
	@docker rmi `docker images |grep $(PROJECT) |xargs -L1 | awk '{print $1}'`


# target: rmvol - remove all volumes in project
.PHONY: rmvol
rmvol:
	@docker volume rm `docker volume ls |grep $(PROJECT) |xargs -L1 | awk "{print $2}"`
# ...




