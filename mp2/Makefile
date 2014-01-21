NVCC=nvcc
LIBWB=$(HOME)/libwb
LIBWB_ARCH=$(LIBWB)/Linux-x86_64
INCL=-I $(LIBWB)
MKREPORT=../mkreport
SM=sm_20

# Uncomment next two lines if using Ocelot emulator
#LIBS=-l wb -l ocelot
#CC=g++

# Uncomment next two lines if using GPU card
LIBS=-l wb -l cuda -l cudart
CC=nvcc

OPT=-O2
#DEBUG=-g

mp2: mp2.o $(LIBWB_ARCH)/libwb.so
	$(CC) mp2.o -L $(LIBWB_ARCH) $(LIBS) -o mp2

mp2.o: mp2.cu $(LIBWB)/wb.h
	$(NVCC) -arch=$(SM) $(DEBUG) $(OPT) $(INCL) mp2.cu -c

ptx: mp2.ptx

mp2.ptx: mp2.cu $(LIBWB)/wb.h
	$(NVCC) --ptx $(OPT) mp2.cu -o mp2.ptx -arch=$(SM) -I $(INCL)

tests: mp2
	for i in 0 1 2 3 4 5 6 7 8 9; do make --no-print-directory test n=$$i; done

test: mp2
	@echo Test ${n}
	./mp2 -e data/${n}/output.raw -i data/${n}/input0.raw,data/${n}/input1.raw -o out${n}.raw -t vector | grep -v cuInit | $(MKREPORT)

data: dataset.zip
	unzip dataset.zip

clean:
	rm -f mp2 mp2.ptx mp2.o out*.raw

setup:
	rm -rf data
	unzip dataset.zip
	cp -b $(LIBWB)/skel/mp2.cu mp2.cu
