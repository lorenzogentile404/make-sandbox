# Evaluate, immediatly and once for all, the current timestamp and store it in a variable
# Lazy evaluation requires the use of = instead
TIMESTAMP     := $(shell date +%d-%m-%Y_%H-%M-%S)

# Explicitly define the default target for the Makefile
# First target in the Makefile is the default target anyway
# If targets from other Makefiles are included first, explicit definition of the default target is required to avoid ambiguity
.DEFAULT_GOAL := help

# Mark targets that do not represent files as .PHONY
.PHONY: help run append-timestamp-to-log clean

# help target displays a help menu with self-documented targets
help: ## Display this help menu with all documented targets
	@echo "Usage: make [target]"
	@echo ""
	@echo "Available targets:"
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z._-]+:.*?## / {printf "  \033[36m%-25s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

# Include the Makefile from the utils directory
include ../utils/Makefile

# run target runs the echo_my_timestamp.sh script, which is generated if it does not exist or it is not up to date with respect to its dependencies (log.txt)
# $< indicates the first dependency
run: echo_my_timestamp.sh ## Run echo_my_timestamp.sh
	@echo "Invoking run at TIMESTAMP=$(TIMESTAMP)"
	@bash ./$<

# echo_my_timestamp.sh target is generated only if it does not exist or it is not up to date with respect to its dependencies (log.txt)
# $@ indicates the target name
echo_my_timestamp.sh: log.txt ## Generates echo_my_timestamp.sh, which prints its own timestamp when executed
	@echo "Invoking echo_my_timestamp.sh at TIMESTAMP=$(TIMESTAMP)"
	@echo "echo My timestamp is TIMESTAMP=$(TIMESTAMP)" > $@

log.txt: ## Generates log.txt if it does not exist
	@echo "Invoking log.txt at TIMESTAMP=$(TIMESTAMP)"
	@touch $@

# append-timestamp-to-logs makes echo_my_timestamp.sh target out of date, so it will be re-generated next time run is invoked
append-timestamp-to-log: ## Append TIMESTAMP to log.txt
	@echo "Invoking append-timestamp-to-log at TIMESTAMP=$(TIMESTAMP)"
	@echo "TIMESTAMP=$(TIMESTAMP)" >> log.txt

# clean_body macro is defined in ../utils/Makefile
clean: ## Clean generated files
	$(call clean_body, echo_my_timestamp.sh log.txt)