PROGRAM=transpose

include ../../common/FORTRAN.defs
include ../../common/PRKVERSION

FCFLAGS  = $(DEFAULT_OPT_FLAGS)
FCFLAGS += -DPRKVERSION=$(PRKVERSION)
FCFLAGS += -DRADIUS=$(RADIUS) $(STARFLAG)

.PHONY: all clean run

all: $(PROGRAM) $(PROGRAM)-omp $(PROGRAM)-coarray $(PROGRAM)-pretty

$(PROGRAM): $(PROGRAM).f90
	$(FC) $(FCFLAGS) $< -o $@

$(PROGRAM)-omp: $(PROGRAM).f90
	$(FC) $(FCFLAGS) $(OPENMPFLAG) $< -o $@

$(PROGRAM)-coarray: $(PROGRAM)-coarray.f90
	$(CAFCOMPILER) $(FCFLAGS) $< $(COARRAYFLAG) -o $@

$(PROGRAM)-pretty: $(PROGRAM)-pretty.f90
	$(FC) $(FCFLAGS) $< -o $@

run: $(PROGRAM)
	$(PROGRAM) 10 4000 32

clean:
	-rm -f *.o
	-rm -f *.i90
	-rm -f *.optrpt
	-rm -f *.dwarf
	-rm -rf *.dSYM
	-rm -f $(PROGRAM)
	-rm -f $(PROGRAM)-omp
	-rm -f $(PROGRAM)-coarray
	-rm -f $(PROGRAM)-pretty

