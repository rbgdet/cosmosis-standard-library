#include ${COSMOSIS_SRC_DIR}/config/compilers.mk
#
#USER_LDFLAGS=-L${GSL_LIB} -lgsl -lgslcblas -lcosmosis -L${FFTW_LIBRARY} -lfftw3
#USER_CFLAGS=-I${GSL_INC} -Wno-deprecated-declarations -I${FFTW_INCLUDE_DIR} -std=c99
#
#OBJS = io.c errorlist.c maths.c cl_to_xi_interface.c
#
#all: nicaea_interface.so
#
#nicaea_interface.so: $(OBJS)
#	$(CC) $(CFLAGS) -shared -o $@ $^ $(LDFLAGS)
#
#test:
#	@echo "Alas, cl_to_xi_nicaea has no tests"
#
#clean:
#	rm -f nicaea_interface.so
#rm -rf nicaea_interface.so.dSYM

############################################################
# cl_to_xi_nicaea/Makefile  (minimal working version)
############################################################
include ${COSMOSIS_SRC_DIR}/config/compilers.mk

# ---- automatically pick up the active Conda prefix ----
PYTHON        ?= python
CONDA_PREFIX  := $(shell $(PYTHON) -c "import sys; print(sys.prefix)")

# ---- GSL paths (already defined by compilers.mk, but keep for clarity) ----
GSL_INC ?= $(CONDA_PREFIX)/include
GSL_LIB ?= $(CONDA_PREFIX)/lib

# ---- FFTW paths ----
FFTW_INCLUDE_DIR ?= $(CONDA_PREFIX)/include
FFTW_LIBRARY     ?= $(CONDA_PREFIX)/lib

# ---- extra flags ----------------------------------------------------------
USER_CFLAGS  = -I$(GSL_INC) -I$(FFTW_INCLUDE_DIR) -std=c99 -Wno-deprecated-declarations
USER_LDFLAGS = -L$(GSL_LIB)  -lgsl -lgslcblas \
	       -L$(FFTW_LIBRARY) -lfftw3 \
	       -L$(COSMOSIS_LIB_DIR) -lcosmosis

CFLAGS  += $(USER_CFLAGS)
LDFLAGS += $(USER_LDFLAGS)

OBJS = io.c errorlist.c maths.c cl_to_xi_interface.c

############################################################
all: nicaea_interface.so

nicaea_interface.so: $(OBJS)
	$(CC) $(CFLAGS) -shared -o $@ $^ $(LDFLAGS)

clean:
	rm -f nicaea_interface.so
	rm -rf nicaea_interface.so.dSYM

.PHONY: all clean
############################################################
