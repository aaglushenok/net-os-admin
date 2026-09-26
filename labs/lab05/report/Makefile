REPORT = report.md
FILTERS = --filter pandoc-crossref --citeproc
OPTIONS = --number-sections
PDF_ENGINE = --pdf-engine=xelatex

all: report.pdf report.docx

report.pdf: $(REPORT)
	pandoc "$(REPORT)" $(FILTERS) $(PDF_ENGINE) $(OPTIONS) -o report.pdf

report.docx: $(REPORT)
	pandoc "$(REPORT)" $(FILTERS) $(OPTIONS) -o report.docx

clean:
	rm -f report.pdf report.docx

.PHONY: all clean
