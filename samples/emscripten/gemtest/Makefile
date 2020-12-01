LIBPD_DIR = ../../..
GEM_DIR = ../../../../Gem
GLU_DIR = ../../../../glu
SRC_FILES = gemtest.c
TARGET = gemtest.html

GEM_LIBS = $(GEM_DIR)/src/Base/.libs/libBase.a $(GEM_DIR)/src/Controls/.libs/libControls.a $(GEM_DIR)/src/Gem/.libs/libGem.a $(GEM_DIR)/src/Geos/.libs/libGeos.a $(GEM_DIR)/src/Manips/.libs/libManips.a $(GEM_DIR)/src/Nongeos/.libs/libNongeos.a $(GEM_DIR)/src/openGL/.libs/libopenGL.a $(GEM_DIR)/src/Particles/.libs/libParticles.a $(GEM_DIR)/src/Pixes/.libs/libPixes.a $(GEM_DIR)/src/plugins/.libs/libplugins.a $(GEM_DIR)/src/RTE/.libs/libRTE.a $(GEM_DIR)/src/Utils/.libs/libUtils.a $(GEM_DIR)/src/Gem_la-Version.o
GLU_LIBS = $(GLU_DIR)/.libs/libGLU.a

CFLAGS = -I$(LIBPD_DIR)/pure-data/src -I$(LIBPD_DIR)/libpd_wrapper -O3
LDFLAGS = -L$(LIBPD_DIR)/build/libs -lpd -Wl,--whole-archive $(GEM_LIBS) -Wl,--no-whole-archive $(GLU_LIBS)

$(TARGET): $(SRC_FILES) test.pd Makefile Gem/
	emcc $(CFLAGS) -o $(TARGET) $(SRC_FILES) \
	-s USE_SDL=2 \
	-s USE_REGAL=1 \
	-s ERROR_ON_UNDEFINED_SYMBOLS=0 \
	--preload-file test.pd \
	--preload-file Gem \
	$(LDFLAGS)

Gem/: $(GEM_DIR)/abstractions/
	rm -rf Gem
	cp -avi $(GEM_DIR)/abstractions/ Gem
