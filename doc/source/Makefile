all: git

clean:
	@echo ""
	@echo "Cleaning Auxiliary files"
	@echo ""
	@- rm -rf __*
	@- rm -rf _minted-manuscript
	@- latexmk -CA
	@echo ""

git: clean
	@echo "Syncing with Overleaf"
	@echo ""
	@- git add --all .
	@- git commit -am "Local Changes"
	@- git pull
	@- git push origin master
	@echo ""
