LATEX = pdflatex
TEXFILES = $(wildcard *.tex)
BIBFILES = $(wildcard *.bib)

MAINFILE = ferguson-proposal

all: $(MAINFILE).pdf

# add *.cls to the list if using a cls
%.pdf: %.tex %.bib *.cls  $(TEXFILES) $(BIBFILES)
	pdflatex $*.tex 
	bibtex --min-crossrefs=20 $*
	pdflatex $*.tex
	pdflatex $*.tex

%.blg: %.bib
	pdflatex $*.tex
	bibtex --min-crossrefs=20 $*
	pdflatex $*.tex

%.toc: %.tex
	pdflatex $*.tex

clean:
	/bin/rm -f $(MAINFILE).pdf *.dvi *.aux *.ps *~ *.log
	/bin/rm -f *.lot *.lof *.toc *.blg *.bbl url.sty *.out

view: 
	pdflatex $(MAINFILE).tex
	acroread  -geometry 1000x1000 $(MAINFILE).pdf

osx:
	pdflatex $(MAINFILE).tex
	open $(MAINFILE).pdf

check:
	pdflatex $(MAINFILE).tex | grep -s -e "multiply" -e "undefined"

upload:
	svn update | grep "At revision" | sed "s/At revision/SVN rev/" > revision.tex
	pdflatex $(MAINFILE).tex
	scp $(MAINFILE).pdf adf@ssh.cs.brown.edu:www/files/$(MAINFILE)-draft.pdf
