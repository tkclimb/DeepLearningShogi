﻿CC = g++
CFLAGS = -std=c++14 -Wextra -Ofast -MMD -MP -fopenmp -DNDEBUG -DHAVE_SSE4 -DHAVE_SSE42 -DHAVE_BMI2 -msse4.2 -mbmi2 -DHAVE_AVX2 -mavx2
LDFLAGS = -lpthread -lcuda -lcudnn -lcudart -lcublas -lz -flto
INCLUDE = -I../usi -I../cppshogi -I../cppshogi -I/usr/local/cuda/include
LIB = -L/usr/local/cuda-10.1/lib64

target = bin/usi
sources = main.cpp mate.cpp dfpn.cpp Message.cpp UctSearch.cpp ZobristHash.cpp nn_fused_wideresnet10.cpp nn_senet10.cpp nn_wideresnet10.cpp nn_wideresnet15.cpp npz.cpp cudnn_dtype.cpp
cppshogi_sources = bitboard.cpp book.cpp common.cpp cppshogi.cpp generateMoves.cpp hand.cpp init.cpp move.cpp mt64bit.cpp position.cpp search.cpp square.cpp usi.cpp
objects = $(addprefix obj/, $(sources:.cpp=.o))
cppshogi_objects = $(addprefix obj/, $(cppshogi_sources:.cpp=.o))

$(target): $(objects) $(cppshogi_objects)
	@[ -d bin ] || mkdir -p bin
	$(CC) -o $@ $^ $(LIB) $(LDFLAGS) $(CFLAGS)

obj/%.o: %.cpp
	@[ -d obj ] || mkdir -p obj
	$(CC) $(CFLAGS) $(INCLUDE) -o $@ -c $<

obj/%.o: ../cppshogi/%.cpp
	@[ -d obj ] || mkdir -p obj
	$(CC) $(CFLAGS) $(INCLUDE) -o $@ -c $<

all: $(target)

clean:
	rm -f $(objects) $(cppshogi_objects) $(target)