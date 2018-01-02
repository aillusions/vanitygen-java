# CC=gcc
LIBS=-lpcre -lcrypto -lm -lpthread
CFLAGS=-ggdb -O3 -Wall
OBJS=vanitygen.o oclvanitygen.o oclengine.o pattern.o util.o groestl.o
PROGS=vanitygen oclvanitygen

PLATFORM=$(shell uname -s)
ifeq ($(PLATFORM),Darwin)
	OPENCL_LIBS=-framework OpenCL
	LIBS+=-L/usr/local/opt/openssl/lib
	CFLAGS+=-I/usr/local/opt/openssl/include
else
	OPENCL_LIBS=-lOpenCL
endif


most: vanitygen oclvanitygen

all: $(PROGS)

vanitygen: vanitygen.o pattern.o util.o groestl.o
	$(CC) $^ -o $@ $(CFLAGS) $(LIBS)

oclvanitygen: oclvanitygen.o oclengine.o pattern.o util.o groestl.o
	$(CC) $^ -o $@ $(CFLAGS) $(LIBS) $(OPENCL_LIBS)

clean:
	rm -f $(OBJS) $(PROGS) $(TESTS) *.oclbin
