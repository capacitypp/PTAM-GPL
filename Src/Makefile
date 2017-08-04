PREFIX=/usr/local/iimlab
BINPREFIX=$(PREFIX)/bin
LIBPREFIX=$(PREFIX)/lib
INCLUDEPREFIX=$(PREFIX)/include
OPENCVFLAGS=$(shell pkg-config --cflags opencv)
OPENCVLIBS=$(shell pkg-config --libs opencv)
CXX=ccache g++ -Wall -Wno-int-in-bool-context -O2 -DEIGEN_NO_DEBUG

.cpp.o:
	$(CXX) -fPIC -c $< $(OPENCVFLAGS)

all: PTAM

so: define.o io.o make_patch.o makevor.o merge1.o merge2.o merge3.o triangle.o global.o delaunay.o
	$(CXX) -shared -fPIC -o libdelaunay.so $^

PTAM: ARDriver.o ATANCamera.o Bundle.o CalibCornerPatch.o CalibImage.o EyeGame.o GLWindow2.o GLWindowMenu.o HomographyInit.o KeyFrame.o main.o Map.o MapMaker.o MapPoint.o MapViewer.o MiniPatch.o PatchFinder.o Relocaliser.o ShiTomasi.o SmallBlurryImage.o System.o Tracker.o VideoSource_Linux_OpenCV.o
	$(CXX) -o PTAM $^ -lGL -lGVars3 -lcvd -llapack $(OPENCVLIBS)

clean:
	rm -f *.o
	rm -f *.so
	rm -f PTAM

install:
	@mkdir -p $(BINPREFIX)
	@mkdir -p $(LIBPREFIX)
	@mkdir -p $(INCLUDEPREFIX)
	@cp -v PTAM $(BINPREFIX)
	@cp -v libdelaunay.so $(LIBPREFIX)
	@cp -v delaunay.h $(INCLUDEPREFIX)

