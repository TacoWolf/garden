public:: true
tags:: #sapling #infrastructure #github #logseq #sync

- > taco: logseq was the answer i wanted the whole time
  taco: it was sitting in front of me
  taco: i pay for it
  taco: i'm just dumb.
  taco: but here we are
	- me, in the [birdcat cafe matrix server](https://chat.birdcat.cafe)
- i'm not changing the title. long urls 5evr.
	- did you know [[mastodon]] urls shorten down to like 32 characters? so this won't matter for my target audience lol
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
		- you're going to want to go to `https://github.com/yourusername/yourrepo/settings/pages`. under here, you're going to want to select your source as `Deploy from a branch`.
		- this will publish your page at `yourusername.github.io/yourrepository`. HOWEVER, you probably want custom dns stuff like i've got setup. so you need to...
-
- # set up the github repository for custom dns
	- your [[dns]] provider is gonna have a different setup depending on what their web interface looks like, so i can't help you too much here. but you're going to need a `CNAME` record that redirects to `yourusername.github.io`. that will point that url to github's servers so it will know what domain it's needing to serve for that request it just got from your dns rerouting.
	- set up a custom domain under your settings page, which is still something like `https://github.com/yourusername/yourrepo/settings/pages`. then input the custom domain and start pushing to your repo. the github robots will [[automagically]] do the work for you. you can see examples of pages being pushed [here](https://github.com/TacoWolf/garden/actions/workflows/publish.yml).
- # look at all of its majesty
	- at the live url. [ta-daaaa!](https://garden.birdcat.cafe)