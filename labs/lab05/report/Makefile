REPORT = report.md
FILTERS = --filter pandoc-crossref --citeproc
OPTIONS = --number-sections
PDF_ENGINE = --pdf-engine=xelatex

all: report.pdf report.docx report.qmd

report.pdf: $(REPORT)
	pandoc "$(REPORT)" $(FILTERS) $(PDF_ENGINE) $(OPTIONS) -o report.pdf

report.docx: $(REPORT)
	pandoc "$(REPORT)" $(FILTERS) $(OPTIONS) -o report.docx

report.qmd: $(REPORT)
	pandoc "$(REPORT)" $(FILTERS) $(OPTIONS) -t markdown -o report.qmd

clean:
	rm -f report.pdf report.docx report.qmd

.PHONY: all clean
