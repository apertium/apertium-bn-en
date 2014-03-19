VERSION=0.1.0
LANG1=bn
LANG2=en
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON = \
	$(PREFIX2).automorf.bin $(PREFIX2).autobil.bin $(PREFIX2).autogen.bin  \
	$(PREFIX1).automorf.bin $(PREFIX1).autobil.bin $(PREFIX1).autogen.bin  \
	$(PREFIX2).t1x.bin $(PREFIX2).t2x.bin $(PREFIX2).t3x.bin \
	$(PREFIX1).t1x.bin $(PREFIX1).t2x.bin $(PREFIX1).t3x.bin

$(PREFIX1).automorf.bin: $(BASENAME).$(LANG1).dix
#	apertium-validate-dictionary $(BASENAME).$(LANG1).dix
	lt-comp lr $(BASENAME).$(LANG1).dix $@

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
#	apertium-validate-dictionary $(BASENAME).$(PREFIX1).dix
	lt-comp lr $(BASENAME).$(PREFIX1).dix $@

$(PREFIX1).autogen.bin: $(BASENAME).$(LANG2).dix
#	apertium-validate-dictionary $(BASENAME).$(LANG2).dix
	lt-comp rl $(BASENAME).$(LANG2).dix $@


$(PREFIX2).automorf.bin: $(BASENAME).$(LANG2).dix
#	apertium-validate-dictionary $(BASENAME).$(LANG2).dix
	lt-comp lr $(BASENAME).$(LANG2).dix $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
#	apertium-validate-dictionary $(BASENAME).$(PREFIX1).dix
	lt-comp rl $(BASENAME).$(PREFIX1).dix $@

$(PREFIX2).autogen.bin: $(BASENAME).$(LANG1).dix
#	apertium-validate-dictionary $(BASENAME).$(LANG1).dix
	lt-comp rl $(BASENAME).$(LANG1).dix $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $(BASENAME).$(PREFIX2).t1x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t1x $@

$(PREFIX2).t2x.bin: $(BASENAME).$(PREFIX2).t2x
	apertium-validate-interchunk $(BASENAME).$(PREFIX2).t2x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t2x $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $(BASENAME).$(PREFIX2).t3x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX2).t3x $@

$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $(BASENAME).$(PREFIX1).t1x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t1x $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $(BASENAME).$(PREFIX1).t2x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t2x $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $(BASENAME).$(PREFIX1).t3x
	apertium-preprocess-transfer $(BASENAME).$(PREFIX1).t3x $@


EXTRA_DIST=$(BASENAME).$(LANG1).dix $(BASENAME).$(PREFIX1).dix \
           $(BASENAME).post-$(LANG1).dix $(BASENAME).post-$(LANG2).dix \
           $(BASENAME).$(LANG2).dix $(BASENAME).$(LANG1).tsx \
           $(BASENAME).$(LANG2).tsx  \
           $(PREFIX2).prob \
           $(PREFIX2)-supervised.make $(PREFIX2)-unsupervised.make \
           $(LANG1)-tagger-data/README $(LANG2)-tagger-data/README \
           $(BASENAME).$(PREFIX2).t1x $(BASENAME).$(PREFIX1).t1x \
           $(BASENAME).$(PREFIX2).t2x $(BASENAME).$(PREFIX1).t2x \
	   $(BASENAME).$(PREFIX2).t3x $(BASENAME).$(PREFIX1).t3x \
           modes.xml

###############################################################################
## Translation modes
###############################################################################

modes/$(PREFIX1).mode: modes.xml
	apertium-validate-modes modes.xml
	apertium-gen-modes modes.xml
	cp *.mode modes/

apertium_bn_endir=$(prefix)/share/apertium/apertium-$(PREFIX1)/
apertium_modesdir=$(prefix)/share/apertium/modes/

apertium_bn_en_DATA=$(TARGETS_COMMON) \
	modes.xml

# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode

install-data-local:
	mv modes modes.bak
	apertium-gen-modes modes.xml $(BASENAME)
	rm -rf modes
	mv modes.bak modes
	test -d $(DESTDIR)$(apertium_modesdir) || mkdir $(DESTDIR)$(apertium_modesdir)
	modes=`xmllint --xpath '//mode[@install="yes"]/@name' modes.xml | sed 's/ *name="\([^"]*\)"/\1.mode /g'`; \
		$(INSTALL_DATA) $$modes $(DESTDIR)$(apertium_modesdir); \
		rm $$modes
	$(INSTALL_DATA) $(BASENAME).$(PREFIX2).t1x $(BASENAME).$(PREFIX1).t1x $(DESTDIR)$(apertium_bn_endir)
	$(INSTALL_DATA) $(BASENAME).$(PREFIX2).t2x $(BASENAME).$(PREFIX1).t2x $(DESTDIR)$(apertium_bn_endir)
	$(INSTALL_DATA) $(BASENAME).$(PREFIX2).t3x $(BASENAME).$(PREFIX1).t3x $(DESTDIR)$(apertium_bn_endir)


CLEANFILES = $(TARGETS_COMMON)
clean-local: 
	-rm -rf .deps modes
