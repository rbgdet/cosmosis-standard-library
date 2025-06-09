#include ${COSMOSIS_SRC_DIR}/config/compilers.mk
#
#USER_LDFLAGS=-L$(GSL_LIB)  -lgsl -lgslcblas -lm -lcosmosis
#USER_CFLAGS=-I$(GSL_INC)
#
#all: emu.so
#
#emu.so: emu.c emu_interface.c params.h
#	${CC}  ${CFLAGS} emu.c emu_interface.c -shared  -o  emu.so ${LDFLAGS}
#
#test:
#	@echo "Alas, cosmic_emu has no tests"
#
#clean:
#	rm -f *.o emu.so
#	rm -rf emu.so.dSYM
#
include ${COSMOSIS_SRC_DIR}/config/compilers.mk

PYTHON?=python
CONDA_PREFIX:=$(shell $(PYTHON) -c "import sys; print(sys.prefix)")
GSL_INC:=$(CONDA_PREFIX)/include
GSL_LIB:=$(CONDA_PREFIX)/lib

# extra search paths
USER_CFLAGS  := -I$(COSMOSIS_SRC_DIR)/cosmosis -I$(GSL_INC)
USER_LDFLAGS := -L$(COSMOSIS_LIB_DIR) -lcosmosis \
                -L$(GSL_LIB)       -lgsl -lgslcblas

# append our extras to the defaults
CFLAGS  := $(CFLAGS)  $(USER_CFLAGS)
LDFLAGS := $(LDFLAGS) $(USER_LDFLAGS)

.PHONY: all clean

all: emu.so

emu.so: emu.c emu_interface.c
	$(CC) $(CFLAGS) -shared -o $@ $^ $(LDFLAGS)

