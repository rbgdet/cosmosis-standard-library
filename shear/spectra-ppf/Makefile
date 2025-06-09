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

# --- locate compilers and global variables ----------------------------------
include ${COSMOSIS_SRC_DIR}/config/compilers.mk    # sets CC,CFLAGS,LDFLAGS…

# --- find GSL inside the current conda env ----------------------------------
PYTHON        ?= python
CONDA_PREFIX  := $(shell $(PYTHON) -c "import sys, pathlib; print(pathlib.Path(sys.prefix))")
GSL_INC       := $(CONDA_PREFIX)/include
GSL_LIB       := $(CONDA_PREFIX)/lib

# --- where libcosmosis.so lives ---------------------------------------------
# (datablock is where the CosmoSIS core dropped its shared library)
COSMOSIS_LIB_DIR ?= $(COSMOSIS_SRC_DIR)/datablock

# --- extra include & link flags ---------------------------------------------
USER_CFLAGS  := -I$(COSMOSIS_SRC_DIR)/cosmosis          \
	-I../limber                            \
	-I$(GSL_INC)

USER_LDFLAGS := -L$(COSMOSIS_LIB_DIR) -lcosmosis       \
	-L../limber       -llimber             \
	-L$(GSL_LIB)      -lgsl -lgslcblas

# propagate our additions to the canonical variables that the rule will use
CFLAGS  += $(USER_CFLAGS)
LDFLAGS += $(USER_LDFLAGS)

# ---------------------------------------------------------------------------
all: interface.so

interface.so: shear_shear.c interface.c ../limber/liblimber.so
	$(CC) $(CFLAGS) -shared -o $@ $^ $(LDFLAGS)

clean:
	$(RM) interface.so interface.so.dSYM

.PHONY: all clean
