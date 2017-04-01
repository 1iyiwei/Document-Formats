EXTENDED-ABSTRACT = extended-abstract
PROCEEDINGS = proceedings

BIB_SOURCES = sample.bib

PAPER_SOURCES := $(wildcard *.tex)
EXTENDED-ABSTRACT_SOURCES = extended-abstract.tex $(PAPER_SOURCES)
PROCEEDINGS_SOURCES = proceedings.tex $(PAPER_SOURCES)

HAND_DIR = figs/handdrawn/
RASTER_DIR = figs/raster/
HAND_FIGS = 
SVG_FIGS = #$(HAND_DIR)/example.svg
RASTER_FIGS = #$(RASTER_DIR)/161.jpg

HAND_EPS = $(HAND_FIGS:.fig=.eps)
HAND_PDF = $(HAND_EPS:.eps=.pdf)
SVG_PDF = $(SVG_FIGS:.svg=.pdf)

ALL_FIGS = $(HAND_FIGS) $(RASTER_FIGS) $(SVG_PDF)

all: extended-abstract proceedings

extended-abstract: $(EXTENDED-ABSTRACT).pdf
proceedings: $(PROCEEDINGS).pdf

%.ps : %.fig
	fig2dev -L ps -c $< > $@

# fig2eps is nice, you can download it from
# http://soliton.science.uva.nl/~kager/figepspdf/fig2eps.htm
%.eps : %.fig
	 ./fig2eps -f $<

%.pdfnoembed : %.eps
	 epstopdf $< --outfile $@

%.pdf : %.pdfnoembed
	ps2pdf13 -dPDFSETTINGS=/prepress $< $@

%.pdf : %.svg
	inkscape $< --export-pdf $@

$(EXTENDED-ABSTRACT).pdf : $(EXTENDED-ABSTRACT_SOURCES) $(ALL_FIGS) $(EXTENDED-ABSTRACT).bbl
	pdflatex $(EXTENDED-ABSTRACT)

$(EXTENDED-ABSTRACT).aux : $(EXTENDED-ABSTRACT_SOURCES) $(ALL_FIGS)
	pdflatex $(EXTENDED-ABSTRACT)

$(EXTENDED-ABSTRACT).bbl : $(EXTENDED-ABSTRACT_SOURCES) $(BIB_SOURCES) $(EXTENDED-ABSTRACT).aux 
	bibtex $(EXTENDED-ABSTRACT)

$(PROCEEDINGS).pdf : $(PROCEEDINGS_SOURCES) $(ALL_FIGS) $(PROCEEDINGS).bbl
	pdflatex $(PROCEEDINGS)

$(PROCEEDINGS).aux : $(PROCEEDINGS_SOURCES) $(ALL_FIGS)
	pdflatex $(PROCEEDINGS)

$(PROCEEDINGS).bbl : $(PROCEEDINGS_SOURCES) $(BIB_SOURCES) $(PROCEEDINGS).aux 
	bibtex $(PROCEEDINGS)

clean:
	rm -f $(EXTENDED-ABSTRACT).pdf $(EXTENDED-ABSTRACT).out $(EXTENDED-ABSTRACT).dvi $(EXTENDED-ABSTRACT).bbl $(EXTENDED-ABSTRACT).aux $(EXTENDED-ABSTRACT).blg $(EXTENDED-ABSTRACT).log $(PROCEEDINGS).pdf $(PROCEEDINGS).out $(PROCEEDINGS).dvi $(PROCEEDINGS).bbl $(PROCEEDINGS).aux $(PROCEEDINGS).blg $(PROCEEDINGS).log $(SVG_PDF)
