###jQuery Git Hooks
Working a lot with jquery and with git, i decided to start a repo of the hooks that i use to save time and automate repetitive activities like minifying and such.

####Pre-Commit
The Problems:

1. Usually by the time I do a commit I want to create minified deployment versions of my scripts. Even with jsmin it can be tedious manually minifying scripts all the time.
2. I'm a fan of automated testing (QUnit ftw). Unfortunately, i'm also a fan of self-calling anonymous-function closures, or:
	(function($) {
		//Code here...
	})(jQuery);
Frustratingly, you can't test functions inside of these closures. So i usually have my dev code set up without them, then add the wrapping closure to the deploy version.
3. Sometimes i add some debug output to my dev code (i.e. console.log) that, while i don't want it in the deploy script, i may want to leave around so that i don't have to re-add it all the time

Enter my Pre-Commit hook

The Solutions:

1. Minifies any *.js file that has been changed in this commit automatically (names it *.min.js)
2. Wraps any *.js file that has been changed in a self-calling annonymous-function closure (that thing i mentioned earlier)
3. Strips out any lines that call console.log

####Installation and Requirements
Pre-Commit uses jsmin (included here). Simple drop the jsmin script somewhere in your path. This is the ruby version, so ruby is also required. If you already have a jsmin installed, that's fine too. As long as the jsmin command is found.

Drop the Pre-Commit hook in your repo, make sure everyone has execute permission

	sudo chmod a+x pre-commit
	
And then you should be good to go.