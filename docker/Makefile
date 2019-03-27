# Defaults

IMAGE := cats

# Help

help:
	@$(MAKE) -pRrq -f $(lastword $(MAKEFILE_LIST)) : 2>/dev/null \
		| awk -v RS= -F: '/^# File/,/^# Finished Make data base/ {if ($$1 !~ "^[#.]") {print $$1}}' \
		| egrep -v -e '^[^[:alnum:]]' -e '^$@$$' | sort -r

CONTEXTS := $(shell find . -name "*jpg" -type f | sed -n 's:.*/\(.*\).jpg:\1:p')

$(addprefix build-, $(CONTEXTS)): build-%:
	docker build -f Dockerfile --build-arg img=$*.jpg -t raelga/$(IMAGE):$* context

$(addprefix run-, $(CONTEXTS)): run-%: build-%
	docker run --rm -p 7080:80 raelga/$(IMAGE):$*

$(addprefix push-, $(CONTEXTS)): push-%:
	docker push raelga/$(IMAGE):$*

all-build: $(addprefix build-, $(CONTEXTS))

all-push: $(addprefix push-, $(CONTEXTS))