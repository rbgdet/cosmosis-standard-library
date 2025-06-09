#include ${COSMOSIS_SRC_DIR}/config/compilers.mk
#
#USER_CFLAGS= -I  ${GSL_INC}
#USER_LDFLAGS=  -lcosmosis -L ${GSL_LIB} -lgsl -lgslcblas
#
#all: interface.so
#
#test:
#	@echo Alas, growth_factor has no tests
#
#interface.so: growthfactor.c  interface.c
#	$(CC) $(CFLAGS)  -shared -o interface.so growthfactor.c  interface.c $(LDFLAGS)
#
#clean:
#	rm -rf interface.so interface.so.dSYM  *.o

include ${COSMOSIS_SRC_DIR}/config/compilers.mk

PYTHON        ?= python
CONDA_PREFIX  := $(shell $(PYTHON) -c "import sys; print(sys.prefix)")
GSL_INC       := $(CONDA_PREFIX)/include
GSL_LIB       := $(CONDA_PREFIX)/lib

# extra search paths
USER_CFLAGS   := -I$(GSL_INC)
USER_LDFLAGS  := -L$(COSMOSIS_LIB_DIR) -lcosmosis \
                 -L$(GSL_LIB)       -lgsl -lgslcblas

# append our extras to the defaults
CFLAGS        := $(CFLAGS) $(USER_CFLAGS)
LDFLAGS       := $(LDFLAGS) $(USER_LDFLAGS)

.PHONY: all clean test

all: interface.so

interface.so: growthfactor.c interface.c
	$(CC) $(CFLAGS) -shared -o $@ $^ $(LDFLAGS)

test:
	@echo "Alas, growth_factor has no tests"

clean:
	rm -f interface.so *.o interface.so.dSYM

