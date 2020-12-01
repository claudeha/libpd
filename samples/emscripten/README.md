# empd

emscripten + libpd

## install

first install and activate the emscripten environment. then

    git clone --recursive https://github.com/claudeha/libpd.git
    cd libpd
    git checkout emscripten
    cd pure-data
    git remote add claudeha https://github.com/claudeha/pure-data.git
    git fetch claudeha
    git checkout claudeha/emscripten
    cd ..
    mkdir build
    cd build
    emcmake cmake .. -DPD_UTILS:BOOL=OFF -DCMAKE_BUILD_TYPE=Release
    emmake make
    cd ../samples/emscripten/pdtest
    emmake make
    cd ../pdtest_gui
    emmake make
    cd ..

## run

    python -m SimpleHTTPServer 8080 &
    firefox http://localhost:8080/pdtest/pdtest.html   # plays automatically
    chromium http://localhost:8080/pdtest/index.html   # click to play

## Gem (advanced!)

as above, then

    cd ../../..
    git clone https://github.com/claudeha/glu.git
    cd glu
    git checkout emscripten
    ./autogen.sh
    GL_CFLAGS="-s USE_REGAL=1 -DAPIENTRY=" GL_LIBS="-s USE_REGAL=1" emconfigure ./configure --enable-static --disable-shared
    GL_CFLAGS="-s USE_REGAL=1 -DAPIENTRY=" GL_LIBS="-s USE_REGAL=1" emmake make
    cd ..
    git clone https://github.com/claudeha/Gem.git
    cd Gem
    git checkout emscripten
    ./autogen.sh
    GL_CFLAGS="-s USE_REGAL=1" GL_LIBS="-s USE_REGAL=1" GLU_CFLAGS="-I$(pwd)/../glu/include" GLU_LIBS="$(pwd)/../glu/.libs/libGLU.a" emconfigure ./configure --enable-static --disable-shared --with-pd="$(pwd)/../libpd/pure-data" --disable-multicontext
    GL_CFLAGS="-s USE_REGAL=1" GL_LIBS="-s USE_REGAL=1" GLU_CFLAGS="-I$(pwd)/../glu/include" GLU_LIBS="$(pwd)/../glu/.libs/libGLU.a" emmake make -k
    cd ../libpd/samples/emscripten/gemtest
    emmake make
    firefox http://localhost:8080/gemtest/gemtest.html   # plays automatically
    chromium http://localhost:8080/gemtest/index.html    # click to play
