include ../../../mk/pitchfork.mk

# Local variables
_NAME             = pbbamr
$(_NAME)_REPO    ?= git://github.com/PacificBiosciences/pbbamr
_WRKSRC           = $(WORKDIR)/$(_NAME)
$(_NAME)_VERSION ?= HEAD
R                := $(shell ../../../bin/checkR $(HAVE_R))
R_LIBS           := $(PREFIX)/lib/R/library:$(shell $(R) --slave --vanilla -e 'cat(.Library)')

# Local works
do-install: $(PREFIX)/var/pkg/$(_NAME)
$(PREFIX)/var/pkg/$(_NAME):
	mkdir -p $(PREFIX)/lib/R/library
	R_LIBS=$(R_LIBS) $(R)script install-pbbamr.R
	cd $(PREFIX) && \
        find lib/R/library -type f > $@
do-distclean:
	cd $(_WRKSRC) && $(GIT) clean -xdf
do-flush:
	rm -rf $(_WRKSRC)
