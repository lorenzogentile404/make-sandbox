# Define a reusable macro function to clean files passed as an argument
# $(1) contains space-separated list of files to remove
define clean-body
	@echo "Invoking \033[31mclean\033[0m at TIMESTAMP=$(TIMESTAMP)"
	@rm -f $(1)
endef
