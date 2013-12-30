################################################################################
# Building slides for "Getting started with R" presentation
#
# You wil need to have R installed (suggested 3.0 or greater) to build
# these slides. You will also need a LaTeX install. If so, just type:
#
# 	$ make
#
# Which will generate r_slides.pdf
#
################################################################################

# Any libraries will be installed locally, and R/Sweave will run using that path.
LIBS = .libraries
RCMD = R_LIBS=../$(LIBS) R --vanilla
RDO  = $(RCMD) -f
Sweave = $(RCMD) CMD Sweave

# clear any existing suffixes
.SUFFIXES:

# save a lot of typing with auto build rules
.SUFFIXES: .Rnw .tex .R .rda .pdf .csv

.Rnw.tex:
	$(Sweave) $(<F)

.R.rda:
	$(RDO) $(<F)

.R.csv:
	$(RDO) $(<F)

.R.pdf:
	$(RDO) $(<F) 

.tex.pdf:
	latexmk -pdf $(<F)

### Default task
all: paper.pdf poster.pdf

interactive:
	R_LIBS=$(LIBS) R --quiet --no-save


################################################################################
# Installing dependencies
################################################################################

INSTALLLIB = $(RCMD) CMD INSTALL --no-multiarch --no-docs --library=$(LIBS)

installpkg = mkdir -p $(LIBS) ; R_LIBS=$(LIBS) R --vanilla -e "install.packages('$(1)', repos = 'http://streaming.stat.iastate.edu/CRAN/')" ; date > $(LIBS)/$(1)/INSTALLED

$(LIBS)/xtable/INSTALLED:
	$(call installpkg,xtable)

################################################################################
# Presentation
################################################################################

