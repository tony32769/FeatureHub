# Minimal makefile for Sphinx documentation

.DEFAULT_TARGET: help

# You can set these variables from the command line.  SPHINXOPTS    = -c ./
SPHINXAPIDOC  = sphinx-apidoc
SPHINXBUILD   = sphinx-build
SPHINXPROJ    = FeatureHub
SOURCEDIR     = src
BUILDDIR      = _build
PROJDIR       = ../src/featurehub

.PHONY: help
help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: clean
clean:
	@if [ "$(BUILDDIR)" != "." ]; then \
	     rm -r "$(BUILDDIR)"; \
	     echo "Removed files."; \
	 else \
	     echo "Remove those files yourself, silly."; \
	 fi

# Catch-all target: route all unknown targets to Sphinx using the new
# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
.PHONY: Makefile
%: Makefile apidoc
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

.PHONY: apidoc
apidoc:
	@$(SPHINXAPIDOC) -o "$(SOURCEDIR)" "$(PROJDIR)" "$(PROJDIR)/tests"

.PHONY: devserver
htmlserver:
	@./devserver.sh "$(BUILDDIR)/html"

.PHONY: stopserver
stopserver:
	@cat server.pid | xargs kill

.PHONY: publish
publish: html
	ghp-import -n -m "Update documentation" -b gh-pages "$(BUILDDIR)/html"
