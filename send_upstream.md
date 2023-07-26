### Links

Kernel.org git repositories
https://git.kernel.org/

Jonathan Iain Cameron, iio tree:
https://git.kernel.org/pub/scm/linux/kernel/git/jic23/iio.git/

Linux Git Repository
https://github.com/torvalds/linux

Linux Kernel Documentation
https://www.kernel.org/doc/html/latest/index.html

Submitting Patches
https://www.kernel.org/doc/html/latest/process/submitting-patches.html

Example of Patch Submission
https://lore.kernel.org/all/20230330102100.17590-1-paul@crapouillou.net/

Patches by Email
https://alblue.bandlem.com/2011/12/git-tip-of-week-patches-by-email.html

Git useful stuff
https://home.regit.org/technical-articles/git-for-the-newbie/

Linux Kernel Archives
https://www.kernel.org/

## Git sendmail

### Git sendmail configuration

Learn to use git send-email
https://git-send-email.io/#step-1

Set git config:

	git config --global --edit

		[sendemail]
			smtpserver = zeus.spd.analog.com
			smtp-encryption = tls
			smtppass = <password>


### Issue


	Command unknown: 'AUTH' at /usr/lib/git-core/git-send-email line 1655.


Solved by removing smtpuser from configs.

### Git send email commands

Format git diff into \<name>.patch

	git format-patch HEAD~1
		=> outputs file <name>.patch
	
Send email to myself for testing:

	git send-email --to="<my_email>" <name>.patch

Send to maintainers

	git send-email --cc-cmd='./scripts/get_maintainer.pl --norolestats 000*' <name>.patch
