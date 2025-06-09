#include ${COSMOSIS_SRC_DIR}/config/compilers.mk
#
#USER_CFLAGS= -I ../limber -I ${GSL_INC}
#USER_LDFLAGS= -L../limber -llimber -lcosmosis -L ${GSL_LIB} -lgsl -lgslcblas 
#
#all: interface.so
#
#interface.so: shear_shear.c interface.c ../limber/liblimber.so
#	$(CC) $(CFLAGS)  -shared -o interface.so shear_shear.c interface.c $(LDFLAGS)
#
#clean:
#	rm -rf interface.so interface.so.dSYM
#
#test:
#	@echo Alas, shear/spectra has no tests

#include ${COSMOSIS_SRC_DIR}/config/compilers.mk
#
#PYTHON        ?= python
#CONDA_PREFIX  := $(shell $(PYTHON) -c "import sys; print(sys.prefix)")
#GSL_INC       := $(CONDA_PREFIX)/include
#GSL_LIB       := $(CONDA_PREFIX)/lib
#
#USER_CFLAGS   = -I$(COSMOSIS_SRC_DIR)/cosmosis/ \
#		-I../limber \
#		-I$(GSL_INC)
#USER_LDFLAGS  = -L$(COSMOSIS_LIB_DIR) -lcosmosis \
#		-L../limber -llimber \
#all: interface.so
#
#
#clean:
#	rm -rf interface.so interface.so.dSYM
#
#test:
#	@echo "Alas, shear/spectra has no tests"
#.PHONY: all clean test

include ${COSMOSIS_SRC_DIR}/config/compilers.mk

PYTHON       ?= python
CONDA_PREFIX := $(shell $(PYTHON) -c "import sys; print(sys.prefix)")
GSL_INC      := $(CONDA_PREFIX)/include
GSL_LIB      := $(CONDA_PREFIX)/lib

# locate your cosmosis library directory
COSMOSIS_LIB_DIR ?= $(COSMOSIS_SRC_DIR)/datablock
# extra include paths
USER_CFLAGS  := -I$(COSMOSIS_SRC_DIR)/cosmosis \
		-I../limber  \
		-I$(GSL_INC)
# extra linker flags
USER_LDFLAGS := -L$(COSMOSIS_LIB_DIR) -lcosmosis \
	-L$(GSL_LIB) -lgsl -lgslcblas
LDFLAGS += $(USER_LDFLAGS)
all: interface.so
interface.so: shear_shear.c interface.c ../limber/liblimber.so
	$(CC) $(CFLAGS) $(USER_CFLAGS) -shared -o $@ $^ $(USER_LDFLAGS)

clean:
	rm -f interface.so

.PHONY: all clean
