include ../../../mk/pitchfork.mk

# Local variables
_NAME             = Rcpp
_WRKSRC           = $(WORKDIR)/$(_NAME)
R                := $(shell ../../../bin/checkR $(HAVE_R))
_tmpvar          := $(if $(shell which $(R)),exists,$(error "unable to run $(R)"))
ifneq ($(origin HAVE_R),undefined)
  R_LIBS         := $(PREFIX)/lib/R/library:$(shell $(HAVE_R) --slave --vanilla -e 'cat(.Library)')
else
  R_LIBS         := $(PREFIX)/lib/R/library:$(shell $(R)      --slave --vanilla -e 'cat(.Library)')
endif

# Local works
do-config: $(_WRKSRC)/install-pbbamr.R
$(_WRKSRC)/install-pbbamr.R:
	mkdir -p $(_WRKSRC)
	echo 'install.packages("Rcpp", repos="http://cran.r-project.org")' > $(_WRKSRC)/install-pbbamr.R
do-install: $(PREFIX)/var/pkg/$(_NAME)
$(PREFIX)/var/pkg/$(_NAME): | do-config
	mkdir -p $(PREFIX)/lib/R/library
	R_LIBS=$(R_LIBS) $(R) -f $(_WRKSRC)/install-pbbamr.R
	cd $(PREFIX) && find lib/R/library/$(_NAME) > $@
do-distclean:
	cd $(_WRKSRC) && $(GIT) clean -xdf
do-flush:
	rm -rf $(_WRKSRC)
