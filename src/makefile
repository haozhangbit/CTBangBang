NVCC=nvcc
CC=gcc

ODIR=obj

IDIR_RECON=../include/
INCLUDES=-I$(IDIR_RECON)

LIBS=-lfftw3 -lm -lctbb_read

CFLAGS=$(INCLUDES) -g

_OBJ=main.o setup.o interp.o preprocessing.o rebin_filter.o rebin_filter_cpu.o backproject.o backproject_cpu.o
OBJ=$(patsubst %,$(ODIR)/%,$(_OBJ));

all: ../ctbangbang

../ctbangbang: $(OBJ)
	(cd obj && $(NVCC) -g -o ../../ctbangbang *.o $(LIBS))

obj/main.o: main.cu $(IDIR_RECON)recon_structs.h $(IDIR_RECON)setup.h $(IDIR_RECON)rebin_filter.h $(IDIR_RECON)backproject.h
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/setup.o: setup.cu $(IDIR_RECON)setup.h
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/interp.o: interp.cu $(IDIR_RECON)interp.h
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/preprocessing.o: preprocessing.cu $(IDIR_RECON)preprocessing.h $(IDIR_RECON)preprocessing.cuh
	$(NVCC) $(CFLAGS) -c -o $@ $<	

obj/rebin_filter.o: rebin_filter.cu $(IDIR_RECON)rebin_filter.h $(IDIR_RECON)rebin_filter.cuh 
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/rebin_filter_cpu.o: rebin_filter_cpu.cu $(IDIR_RECON)rebin_filter_cpu.h 
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/backproject.o: backproject.cu $(IDIR_RECON)backproject.cuh
	$(NVCC) $(CFLAGS) -c -o $@ $<

obj/backproject_cpu.o: backproject_cpu.cu $(IDIR_RECON)backproject_cpu.h
	$(NVCC) $(CFLAGS) -c -o $@ $<

.PHONY: all test clean

clean:
	rm obj/*.o; rm -rf ../*~

