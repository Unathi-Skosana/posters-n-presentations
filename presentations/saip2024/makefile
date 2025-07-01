.PHONY: main clean FORCE

main: p.pdf p-notes.pdf

%.pdf: FORCE
	latexmk -pvc -pdflatex='xelatex -interaction nonstopmode' -pdf $(patsubst %.pdf,%.tex,$@)

clean:
	latexmk -pdf -C
