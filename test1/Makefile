
#CC = clang++
CC = c++

CFLAGS = -g -O2 -std=c++11 -DGTEST_USE_OWN_TR1_TUPLE -I.. -I. -Wall -Wextra
OPENSSL_SUPPORT = -DCPPHTTPLIB_OPENSSL_SUPPORT -I/usr/local/opt/openssl/include -L/usr/local/opt/openssl/lib -lssl -lcrypto
V8_SUPPORT = -I/opt/libv8/include -L/opt/libv8/lib/ -Wl,-rpath,/opt/libv8/lib/ -Wl,-rpath,/opt/libv8/lib/ -lv8_libbase -lv8_libplatform -lv8
ZLIB_SUPPORT = -DCPPHTTPLIB_ZLIB_SUPPORT -lz

all : test
	./test

test : test.cpp ../httplib.h Makefile cert.pem
	$(CC) -o test $(CFLAGS) test.cpp $(OPENSSL_SUPPORT) $(ZLIB_SUPPORT) $(V8_SUPPORT) -lpthread 

cert.pem:
	openssl genrsa 2048 > key.pem
	openssl req -new -batch -config test.conf -key key.pem | openssl x509 -days 3650 -req -signkey key.pem > cert.pem

clean:
	rm -f test *.pem
