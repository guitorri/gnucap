GNUCAP = LD_LIBRARY_PATH=$(top_builddir)/lib/.libs:$(top_builddir)/apps/.libs $(top_builddir)/main/gnucap

check: gnucap-run

gnucap-run:
	echo end | $(GNUCAP)

.PHONY: check
