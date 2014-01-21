LIBWB=$(HOME)/libwb
LIBWB_ARCH=$(LIBWB)/Linux-x86_64
INCL=$(LIBWB)
NVCC=nvcc

# Uncomment if using Ocelot emulator
#CC=g++
#LIBS=-l wb -l cuda -l ocelot

# Uncomment if using GPU card
LIBS=-l wb -l cuda -l cudart
CC=nvcc

OPT=-O2
#DEBUG=-g

mp0: mp0.o $(LIBWB_ARCH)/libwb.so
	$(CC) mp0.o -o mp0 -L $(LIBWB_ARCH) $(LIBS)

mp0.o: mp0.cu $(LIBWB)/wb.h
	$(NVCC) $(DEBUG) $(OPT) -arch=sm_20 -I $(INCL) mp0.cu -c

test: mp0
	./mp0 | ../mkreport

clean:
	rm -f mp0 mp0.o
