# Build the questionnaires and answer keys.
#
#   make all      -> all six PDFs
#   make student  -> the four documents handed to students
#   make keys     -> the two internal answer keys
#   make clean    -> remove build artefacts, keep the PDFs
#   make distclean-> remove build artefacts and the PDFs

LATEXMK := latexmk -pdf -interaction=nonstopmode -halt-on-error -file-line-error

STUDENT := pre_form_a pre_form_b post_form_a post_form_b
KEYS    := key_form_a key_form_b
ALLDOCS := $(STUDENT) $(KEYS)

.PHONY: all student keys clean distclean $(ALLDOCS)

all: student keys

student: $(addsuffix .pdf,$(STUDENT))

keys: $(addsuffix .pdf,$(KEYS))

# Every document depends on the shared parts, so touching one part rebuilds all.
COMMON := $(wildcard common/*.tex)

%.pdf: %.tex $(COMMON)
	$(LATEXMK) $<

clean:
	latexmk -c $(addsuffix .tex,$(ALLDOCS))
	rm -f *.aux *.log *.out *.fls *.fdb_latexmk

distclean: clean
	rm -f $(addsuffix .pdf,$(ALLDOCS))
