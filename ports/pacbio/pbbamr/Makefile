include ../../../mk/pitchfork.mk

# Local variables
_NAME             = pbbamr
$(_NAME)_REPO    ?= git://github.com/PacificBiosciences/pbbamr
_WRKSRC           = $(WORKDIR)/$(_NAME)
$(_NAME)_VERSION ?= HEAD
R                := $(shell ../../../bin/checkR $(HAVE_R))
R_LIBS           := $(PREFIX)/lib/R/library:$(shell $(R) --slave --vanilla -e 'cat(.Library)')

# Local works
do-extract:
do-fetch: $(_WRKSRC)
$(_WRKSRC):
ifeq ($(wildcard $($(_NAME)_REPO)),)
	$(GIT) clone $($(_NAME)_REPO) $@
	cd $(_WRKSRC) && $(GIT) checkout $($(_NAME)_VERSION)
else
	ln -sfn $($(_NAME)_REPO) $(_WRKSRC)
endif
do-install: $(PREFIX)/var/pkg/$(_NAME)
$(PREFIX)/var/pkg/$(_NAME):
	mkdir -p $(PREFIX)/lib/R/library
	R_LIBS=$(R_LIBS) $(R) CMD INSTALL $(_WRKSRC)
	cd $(PREFIX) && find lib/R/library/$(_NAME) > $@
do-distclean:
	cd $(_WRKSRC) && $(GIT) clean -xdf
do-flush:
	rm -rf $(_WRKSRC)
