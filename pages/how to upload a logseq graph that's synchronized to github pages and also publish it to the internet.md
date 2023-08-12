public:: true
tags:: #seed #infrastructure #github #logseq sync

- i'm not changing the title.
- # set up [[logseq]]
	- or whatever your [[personal knowledge management]] tool of choice is.
- # create a new [[github]] [[repository]]
	- you'll be using this to synchronize your notes in the cloud.
	- i keep my notes in [this repo](https://github.com/TacoWolf/garden).
	- i use [[logseq]]'s auto commit functionality to do the heavy lifting for me.
- # set up the github auto publish file
	- there's a [github action in the marketplace](https://github.com/marketplace/actions/logseq-publish-spa); that'll [[take you to the mountain]]. you can just copy and paste the one that's there, no tweaking needed. here's a copy just in case:
		- ```
		  on: [push]
		  
		  permissions:
		    contents: write
		  jobs:
		    test:
		      runs-on: ubuntu-latest
		      name: Publish Logseq graph
		      steps:
		        - uses: actions/checkout@v3
		        - uses: logseq/publish-spa@v0.2.0
		        - name: add a nojekyll file # to make sure asset paths are correctly identified
		          run: touch $GITHUB_WORKSPACE/www/.nojekyll
		        - name: Deploy 🚀
		          uses: JamesIves/github-pages-deploy-action@v4
		          with:
		            folder: www
		  ```
-
- this will publish your page at `yourusername.github.io/yourrepository`. HOWEVER, you probably want custom dns stuff like i've got setup. so you need to...
-
- # set up the github repository for custom dns
	- you're going to want to go to `https://github.com/yourusername/yourrepo/settings/pages`. under here, you're going to want to select your source as `Deploy from a branch`. the
-