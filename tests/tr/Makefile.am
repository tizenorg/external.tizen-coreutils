# Make coreutils tests.					-*-Makefile-*-

# Copyright (C) 1997, 1998, 2000, 2003, 2004, 2006 Free Software
# Foundation, Inc.

# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
# 02110-1301, USA.

##test-files-begin
x = tr
explicit =
maint_gen = 1.I 1.X 2.I 2.X 3.I 3.X 4.I 4.X 5.I 5.X 6.I 6.X 7.I 7.X 8.I 8.X \
9.I 9.X a.I a.X b.I b.X c.I c.X d.I d.X e.I e.X f.I f.X g.I g.X h.I h.X i.I \
i.X j.I j.X k.I k.X l.I l.X m.I m.X n.I n.X o.I o.X p.I p.X q.I q.X r.I r.X \
s.I s.X t.I t.X u.I u.X v.I v.X w.I w.X x.I x.X y.I y.X z.I z.X range-a-a.I \
range-a-a.X null.I null.X upcase.I upcase.X dncase.I dncase.X rep-cclass.I \
rep-cclass.X rep-1.I rep-1.X rep-2.I rep-2.X rep-3.I rep-3.X o-rep-1.I \
o-rep-1.X o-rep-2.I o-rep-2.X esc.I esc.X bs-055.I bs-055.X bs-at-end.I \
bs-at-end.X ross-0a.I ross-0a.X ross-0b.I ross-0b.X ross-1a.I ross-1a.X \
ross-1b.I ross-1b.X ross-2.I ross-2.X ross-3.I ross-3.X ross-4.I ross-4.X \
ross-5.I ross-5.X ross-6.I ross-6.X empty-eq.I empty-eq.X empty-cc.I \
empty-cc.X repeat-bs-9.I repeat-bs-9.X repeat-0.I repeat-0.X repeat-zeros.I \
repeat-zeros.X repeat-compl.I repeat-compl.X repeat-xC.I repeat-xC.X \
fowler-1.I fowler-1.X
run_gen = 1.O 1.E 2.O 2.E 3.O 3.E 4.O 4.E 5.O 5.E 6.O 6.E 7.O 7.E 8.O 8.E 9.O \
9.E a.O a.E b.O b.E c.O c.E d.O d.E e.O e.E f.O f.E g.O g.E h.O h.E i.O i.E \
j.O j.E k.O k.E l.O l.E m.O m.E n.O n.E o.O o.E p.O p.E q.O q.E r.O r.E s.O \
s.E t.O t.E u.O u.E v.O v.E w.O w.E x.O x.E y.O y.E z.O z.E range-a-a.O \
range-a-a.E null.O null.E upcase.O upcase.E dncase.O dncase.E rep-cclass.O \
rep-cclass.E rep-1.O rep-1.E rep-2.O rep-2.E rep-3.O rep-3.E o-rep-1.O \
o-rep-1.E o-rep-2.O o-rep-2.E esc.O esc.E bs-055.O bs-055.E bs-at-end.O \
bs-at-end.E ross-0a.O ross-0a.E ross-0b.O ross-0b.E ross-1a.O ross-1a.E \
ross-1b.O ross-1b.E ross-2.O ross-2.E ross-3.O ross-3.E ross-4.O ross-4.E \
ross-5.O ross-5.E ross-6.O ross-6.E empty-eq.O empty-eq.E empty-cc.O \
empty-cc.E repeat-bs-9.O repeat-bs-9.E repeat-0.O repeat-0.E repeat-zeros.O \
repeat-zeros.E repeat-compl.O repeat-compl.E repeat-xC.O repeat-xC.E \
fowler-1.O fowler-1.E
##test-files-end

EXTRA_DIST = Test.pm $x-tests $(explicit) $(maint_gen)
noinst_SCRIPTS = $x-tests
TESTS_ENVIRONMENT = \
  CU_TEST_NAME=`basename $(abs_srcdir)`,$$tst \
  PATH="$(VG_PATH_PREFIX)`pwd`/../../src$(PATH_SEPARATOR)$$PATH"

editpl = sed -e 's,@''PERL''@,$(PERL),g' -e 's,@''srcdir''@,$(srcdir),g'

TESTS = $x-tests

mk_script = $(srcdir)/../mk-script
$(srcdir)/$x-tests: $(mk_script) Test.pm Makefile.am
	test '$x' = test && prog=../../src/$x || prog=$x; \
	$(PERL) -I$(srcdir) -w -- $(mk_script) $(srcdir) $$prog > $@.n
	mv $@.n $@
	chmod 755 $@

MAINTAINERCLEANFILES = $x-tests $(maint_gen)
CLEANFILES = $(run_gen)

check: $(maint_gen)

$(srcdir)/Makefile.am: ../Makefile.am.in Test.pm $(mk_script)
	rm -f $@ $@t
	sed -n '1,/^##test-files-begin/p' $(srcdir)/../Makefile.am.in > $@t
	tool=`echo $(subdir)|sed 's/^tests.//;s/-test//'`; \
	  echo "x = $$tool" >> $@t
	$(PERL) -I$(srcdir) -w -- $(mk_script) $(srcdir) --list >> $@t
	sed -n '/^##test-files-end/,$$p' $(srcdir)/../Makefile.am.in >> $@t
	chmod -w $@t
	mv $@t $@
