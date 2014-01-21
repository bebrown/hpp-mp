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

mp4: mp4.o $(LIBWB_ARCH)/libwb.so
	$(CC) mp4.o -L $(LIBWB_ARCH) $(LIBS) -o mp4

mp4.o: mp4.cu $(LIBWB)/wb.h
	$(NVCC) -arch=$(SM) $(DEBUG) $(OPT) $(INCL) mp4.cu -c

ptx: mp4.ptx

mp4.ptx: mp4.cu $(LIBWB)/wb.h
	$(NVCC) --ptx $(OPT) mp4.cu -o mp4.ptx -arch=$(SM) -I $(INCL)

tests: mp4
	for i in 0 1 2 3 4 5 6 7 8 9; do make --no-print-directory test n=$$i; done

test: mp4
	@echo Test ${n}
	./mp4 -e data/${n}/output.ppm -i data/${n}/input0.ppm,data/${n}/input1.csv -o out${n}.ppm -t image | grep -v cuInit | $(MKREPORT)

data: dataset.zip
	unzip dataset.zip

clean:
	rm -f mp4 mp4.ptx mp4.o out*.raw

setup:
	rm -rf data
	unzip dataset.zip
	cp -b $(LIBWB)/skel/mp4.cu mp4.cu
