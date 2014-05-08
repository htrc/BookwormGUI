EOM_REGEX='1 s:^\xef\xbb\xbf::'
COM_REGEX1='s/^\[[a-z]\].*$$//'
COM_REGEX2="s/\[[a-z]\]//g"
IMG_REGEX='s/<img src=\"images/<img class=\"img\-responsive\" src=\"images/g'

all: clean info.html help.html
.PHONY: all

gdocs:
	curl -o $(FILE).md '$(URL)'
	sed -i.bak -e '1 s:^\xef\xbb\xbf::' \
		-e "s/^\[[a-z]\].*$$//" \
		-e "s/\[[a-z]\]//g" $(NAME).md

info.md:
	curl -o $@ 'https://docs.google.com/document/d/1xZZmR7d-wxa2iOl80CQ30AIMhHuc0D4D6x_TyRGJyFg/export?format=txt&id=1xZZmR7d-wxa2iOl80CQ30AIMhHuc0D4D6x_TyRGJyFg&token=AC4w5VjYkKUUwHzXedwDyUTL6YVRNVSlQA%3A1399301866774'
	sed -i.bak -e $(EOM_REGEX) -e $(COM_REGEX1) -e $(COM_REGEX2) $@
		
help.md:
	curl -o $@ 'https://docs.google.com/document/d/1SgkCD6gWyPVj_XggRKUL8KA8izrsrNgRN_sPOPJfaCM/export?format=txt&id=1SgkCD6gWyPVj_XggRKUL8KA8izrsrNgRN_sPOPJfaCM&token=AC4w5Vg-pilQQjKZy2nmVhqv_Ewm1_YILQ%3A1399565049565'
	sed -i.bak -e $(EOM_REGEX) -e $(COM_REGEX1) -e $(COM_REGEX2) $@

info.html: info.md
	pandoc -o $@ --template=docs-template.html $<
	sed -i.bak $(IMG_REGEX) $@
    
help.html: help.md
	pandoc -o $@ --template=docs-template.html $<
	sed -i.bak $(IMG_REGEX) $@

clean:
	rm -f info.md
	rm -f help.md
	rm -f *.bak

