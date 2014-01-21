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

mp3: mp3.o $(LIBWB_ARCH)/libwb.so
	$(CC) mp3.o -L $(LIBWB_ARCH) $(LIBS) -o mp3

mp3.o: mp3.cu $(LIBWB)/wb.h
	$(NVCC) -arch=$(SM) $(DEBUG) $(OPT) $(INCL) mp3.cu -c

ptx: mp3.ptx

mp3.ptx: mp3.cu $(LIBWB)/wb.h
	$(NVCC) --ptx $(OPT) mp3.cu -o mp3.ptx -arch=$(SM) -I $(INCL)

tests: mp3
	for i in 0 1 2 3 4 5 6 7 8 9; do make --no-print-directory test n=$$i; done

test: mp3
	@echo Test ${n}
	./mp3 -e data/${n}/output.raw -i data/${n}/input0.raw,data/${n}/input1.raw -o out${n}.raw -t matrix | grep -v cuInit | $(MKREPORT)

data: dataset.zip
	unzip dataset.zip

clean:
	rm -f mp3 mp3.ptx mp3.o out*.raw

setup:
	rm -rf data
	unzip dataset.zip
	cp -b $(LIBWB)/skel/mp3.cu mp3.cu
