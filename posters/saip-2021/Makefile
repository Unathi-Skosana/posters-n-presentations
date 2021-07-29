.PHONY: all clean prepare main release preview

all: prepare main release preview

main: build/poster.pdf 

build/poster.pdf: poster.tex
	latexmk -f -quiet -output-directory="./build"

preview:
	latexmk -pvc

clean:
	rm -rf build submission
	latexmk -c

prepare:
	mkdir -p build release 

release:
	cp build/*.pdf release 
