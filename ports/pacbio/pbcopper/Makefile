include ../../../mk/pitchfork.mk

# CXX check
include ../../../mk/chkcxx.mk

# Local variables
_NAME            = pbcopper
$(_NAME)_REPO   ?= git://github.com/PacificBiosciences/$(_NAME)
_WRKSRC          = $(WORKDIR)/$(_NAME)
$(_NAME)_VERSION?= HEAD

# Local works
do-fetch: $(_WRKSRC)
$(_WRKSRC):
ifeq ($(wildcard $($(_NAME)_REPO)),)
	$(GIT) clone $($(_NAME)_REPO) $@
	cd $(_WRKSRC) && $(GIT) checkout $($(_NAME)_VERSION)
	cd $(_WRKSRC)/include/pbcopper/json/internal && $(CURL) -L -O https://raw.githubusercontent.com/nlohmann/json/f86fe57c18c8e97ce3665380dc6cf46f8e42a36f/src/json.hpp
else
	ln -sfn $($(_NAME)_REPO) $(_WRKSRC)
endif
do-config: $(_WRKSRC)/_build/Makefile
$(_WRKSRC)/_build/Makefile: | do-fetch
	mkdir -p $(_WRKSRC)/_build
	cd $(_WRKSRC)/_build \
     && $(CMAKE) \
          -Dpbcopper_build_tests=OFF \
          -DZLIB_INCLUDE_DIRS=$(PREFIX)/include \
          -DZLIB_LIBRARIES=$(PREFIX)/lib/libz.so \
          -DBoost_INCLUDE_DIRS=$(BOOST_ROOT)/include \
        ..
do-build:
	cd $(_WRKSRC)/_build && $(MAKE)
do-install: $(PREFIX)/var/pkg/$(_NAME)
$(PREFIX)/var/pkg/$(_NAME): | do-build
	rsync -ax $(_WRKSRC)/lib/libpbcopper.a $(PREFIX)/lib/
	rsync -ax $(_WRKSRC)/include/pbcopper  $(PREFIX)/include/
	@echo lib/libpbcopper.a > $@ 
	@cd $(PREFIX) && find include/pbcopper -type f >> $@
do-clean:
	$(MAKE) -C $(_WRKSRC)/_build clean
do-distclean:
	cd $(_WRKSRC) && $(GIT) clean -xdf
do-flush:
	rm -rf $(_WRKSRC)
