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
#LIBS=-l wb -l cuda -l cudart
#CC=nvcc

OPT=-O2
#DEBUG=-g

mp1: mp1.o $(LIBWB_ARCH)/libwb.so
	$(CC) mp1.o -L $(LIBWB_ARCH) $(LIBS) -o mp1

mp1.o: mp1.cu $(LIBWB)/wb.h
	$(NVCC) -arch=$(SM) $(DEBUG) $(OPT) $(INCL) mp1.cu -c

ptx: mp1.ptx

mp1.ptx: mp1.cu $(LIBWB)/wb.h
	$(NVCC) --ptx $(OPT) mp1.cu -o mp1.ptx -arch=$(SM) -I $(INCL)

tests: mp1
	for i in 0 1 2 3 4 5 6 7 8 9; do make --no-print-directory test n=$$i; done

test: mp1
	@echo Test ${n}
	./mp1 -e data/${n}/output.raw -i data/${n}/input0.raw,data/${n}/input1.raw -o out${n}.raw -t vector | grep -v cuInit | $(MKREPORT)

data: dataset.zip
	unzip dataset.zip

clean:
	rm -f mp1 mp1.ptx mp1.o out*.raw

setup:
	rm -rf data
	unzip dataset.zip
	cp -b $(LIBWB)/skel/mp1.cu mp1.cu
