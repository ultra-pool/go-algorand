all:	TEAL_opcodes.md teal.tmLanguage.json README.md fields_string.go

# Location of algorandfoundation/specs repo. (Optional)
SPECS := ../../../../specs
# Location of algorand/docs repo. (Optional)
DOCS :=  ../../../../docs

TEAL_opcodes.md teal.tmLanguage.json:	fields_string.go ../../../cmd/opdoc/opdoc.go ../../../cmd/opdoc/tmLanguage.go eval.go assembler.go doc.go opcodes.go
	go run ../../../cmd/opdoc/opdoc.go ../../../cmd/opdoc/tmLanguage.go
	@if [ -e $(SPECS)/dev/TEAL_opcodes.md ]; then \
		sed '/^$$/q' $(SPECS)/dev/TEAL_opcodes.md | cat - TEAL_opcodes.md > opcodes.spec; \
		mv opcodes.spec $(SPECS)/dev/TEAL_opcodes.md; \
		echo "TEAL_opcodes.md updated in specs repo"; \
	fi
	@if [ -e $(DOCS)/docs/reference/teal/opcodes.md ]; then \
		sed 's/^# /title: /g' TEAL_opcodes.md > $(DOCS)/docs/reference/teal/opcodes.md; \
		echo "opcodes.md updated in docs repo"; \
	fi

fields_string.go:	fields.go
	go generate

README.md:	TEAL_opcodes.md README_in.md
	python merge.py > README.md
	@if [ -e $(SPECS)/dev/TEAL.md ]; then \
		sed '/^$$/q' $(SPECS)/dev/TEAL.md | cat - README.md > teal.spec; \
                mv teal.spec $(SPECS)/dev/TEAL.md; \
		echo "TEAL.md updated in specs repo"; \
	fi
	@if [ -e $(DOCS)/docs/reference/teal/specification.md ]; then \
		sed 's/^# /title: /g' README.md > $(DOCS)/docs/reference/teal/specification.md; \
		echo "specification.md updated in docs repo"; \
	fi
