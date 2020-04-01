CPP = /usr/bin/clang++
INCPATHS = -I/usr/include -I/home/nasrinakbari/sequre/ntl/include
CFLAGS = -g -Wall -O1 $(INCPATHS) -march=native -std=c++11 -pthread
LDLIBS = -lssl -lcrypto -lgmp -lm -ldl /home/nasrinakbari/sequre/ntl/src/ntl.a
LDPATH = -L/usr/lib

BUILD = build
PROGS = bin

SRC = crypto.cpp connect.cpp aesstream.cpp mpc.cpp param.cpp
PROGNAMES = DataSharingClient GwasClient LogiRegClient GenerateKey

OBJPATHS = $(patsubst %.cpp,$(BUILD)/%.o, $(SRC))
TESTPATHS = $(addprefix $(PROGS)/, $(PROGNAMES))

all: $(OBJPATHS) $(TESTPATHS)

obj: $(OBJPATHS)

$(BUILD):
	mkdir -p $(BUILD)

$(PROGS):
	mkdir -p $(PROGS)

$(BUILD)/%.o: %.cpp *.h | $(BUILD)
	$(CPP) $(CFLAGS) -o $@ -c $<

$(PROGS)/%: %.cpp $(OBJPATHS) $(PROGS)
	$(CPP) $(CFLAGS) -o $@ $< $(LDPATH) $(OBJPATHS) $(LDLIBS)

clean:
	rm -rf $(BUILD) $(PROGS) *~
