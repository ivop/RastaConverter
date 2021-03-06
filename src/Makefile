
.SUFFIXES:

.SUFFIXES: .cpp .o .o-pg .o-pu

SOURCES 	= CommandLineParser.cpp  config.cpp  main.cpp  rasta.cpp  rgb.cpp \
			  Distance.cpp Evaluator.cpp mt19937int.cpp pch.cpp Program.cpp \
			  TargetPicture.cpp

CXX			= g++

CXXFLAGS 	= -c -O3 -W -Wall -Wextra -pedantic -Wcast-align -Wcast-qual -Wctor-dtor-privacy -Wdisabled-optimization -Wformat=2 -Winit-self -Wlogical-op -Wmissing-include-dirs -Wnoexcept -Woverloaded-virtual -Wredundant-decls -Wsign-promo -Wstrict-null-sentinel -Wstrict-overflow=5 -std=c++0x 
LDFLAGS 	=
LIBS	 	= -lalleg -lfreeimage -lX11 -lXcursor -lXpm -lXxf86vm -lpthread
OBJECTS 	= $(SOURCES:.cpp=.o)

CXXFLAGSPG  = $(CXXFLAGS) -pg -fprofile-generate
LDFLAGSPG   = $(LDFLAGS) -pg
LIBSPG      = $(LIBS) -lgcov
OBJECTSPG 	= $(SOURCES:.cpp=.o-pg)
GCDA		= $(SOURCES:.cpp=.gcda)

CXXFLAGSPU  = $(CXXFLAGS) -fprofile-use
LDFLAGSPU   = $(LDFLAGS)
LIBSPU      = $(LIBS)
OBJECTSPU 	= $(SOURCES:.cpp=.o-pu)

EXECUTABLE	= rastaconv

all: $(EXECUTABLE)

pg: $(EXECUTABLE)-pg

pu: $(EXECUTABLE)-pu

$(EXECUTABLE): $(OBJECTS) 
	$(CXX) $(LDFLAGS) $(OBJECTS) -o $@ $(LIBS)

$(EXECUTABLE)-pg: $(OBJECTSPG)
	$(CXX) $(LDFLAGSPG) $(OBJECTSPG) -o $@ $(LIBSPG)

$(EXECUTABLE)-pu: $(OBJECTSPU)
	$(CXX) $(LDFLAGSPU) $(OBJECTSPU) -o $@ $(LIBSPU)

.cpp.o:
	$(CXX) $(CXXFLAGS) $< -o $@

.cpp.o-pg:
	$(CXX) $(CXXFLAGSPG) $< -o $@

.cpp.o-pu:
	$(CXX) $(CXXFLAGSPU) $< -o $@

$(OBJECTS): CommandLineParser.h  EpochTypes.h rgb.h config.h ErrorConstants.h  rasta.h  string_conv.h

clean:
	rm -f *~ $(OBJECTS) $(OBJECTSPG) $(GCDA) $(OBJECTSPU) $(EXECUTABLE) $(EXECUTABLE)-pg $(EXECUTABLE)-pu
