EXEC            = netcalc
SYMLINK         = ipcalc
TESTS           = testit.sh
EXTRA_DIST      = configure README LICENSE
doc_DATA        = README LICENSE
dist_man1_MANS  = $(EXEC).1
bin_PROGRAMS    = $(EXEC)
netcalc_SOURCES = netcalc.c netcalc.h output.c output.h misc.c strlcpy.c strlcat.c

# Compat rule for Travis, default automake is "make check" for autotests
test: check

# Hook in to install to add netcalc --> ipcalc symlink
install-exec-hook:
	(cd $(DESTDIR)$(bindir); $(LN_S) $(EXEC) $(SYMLINK))

## Target to run when building a release
release: dist
	@for file in $(DIST_ARCHIVES); do	\
		md5sum $$file > ../$$file.md5;	\
	done
	@mv $(DIST_ARCHIVES) ../
	@echo
	@echo "Resulting release files:"
	@echo "================================================================="
	@for file in $(DIST_ARCHIVES); do					\
		printf "$$file    \tDistribution tarball\n";			\
		printf "$$file.md5\t"; cat ../$$file.md5 | cut -f1 -d' ';	\
	done
