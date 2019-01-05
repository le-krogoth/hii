NAME = hii
VERSION ?= unknown

PREFIX ?= /usr/local
BINDIR ?= $(PREFIX)/bin
MANDIR ?= $(PREFIX)/share/man
DOCDIR ?= $(PREFIX)/share/doc/$(NAME)

IMPORTPATH = src/github.com/nmeum/$(NAME)
export GOPATH=$(CURDIR)

$(NAME): $(IMPORTPATH)
	cd $< && env PWD="$(CURDIR)/$(IMPORTPATH)" go build -o $@
$(IMPORTPATH): $(GOPATH)
	mkdir -p $(shell dirname $@)
	ln -fs $< $@

install: $(NAME) $(NAME).1 README.md
	install -Dm755 $(NAME) "$(DESTDIR)$(BINDIR)/$(NAME)"
	install -Dm644 $(NAME).1 "$(DESTDIR)$(MANDIR)/man1/$(NAME).1"
	install -Dm644 README.md "$(DESTDIR)$(DOCDIR)/README.md"

dist:
	mkdir -p $(NAME)-$(VERSION)
	cp -R hii.go hii.1 README.md LICENSE.md vendor $(NAME)-$(VERSION)
	find $(NAME)-$(VERSION) -name '.git' -exec rm -rf {} +
	tar -czf $(NAME)-$(VERSION).tar.gz $(NAME)-$(VERSION)
	rm -rf $(NAME)-$(VERSION)

.PHONY: install dist $(NAME)
