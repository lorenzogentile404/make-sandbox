# Define a reusable macro function to clean files passed as an argument
# $(1) contains space-separated list of files to remove
define clean-body
	@echo "Invoking $(call red,clean) at TIMESTAMP=$(TIMESTAMP)"
	@rm -f $(1)
endef

# Define reusable in-line macros functions to print text in red or yellow color
red    = \033[31m$(1)\033[0m
yellow = \033[33m$(1)\033[0m