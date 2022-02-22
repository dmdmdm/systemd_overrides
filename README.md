# systemd_overrides

Increased sandboxing and permission-limiting for selected Linux services
 
## Intro

These are working sandboxing/security override.conf files for systemd services to reduce
what they are allowed to do without breaking their normal functions.
I selected services I understand and interact with the outside world.
I went down the man page and considered every option that applied.
Sometimes I had to back-out options when they stopped the service from working.

I hope these are useful for some other people.

## Services that run programs

Some services, like atd and crond let users/programs run arbitrary commands.
So locked down those services to what the service itself needs plus what the commands
I run need.  So you might need to change those.

The CGI, PHP, etc scripts that your installation of Apache runs
need to be allowed too.

## How to use

This are *override* files -- in general an override.conf file can override (replace)
any unit option but here we have only added sandbox/security options.
Do NOT modify the <service>.unit file that came with the package.
Instead do:
	
	systemctl edit <service>

You'll be placed in the Nano editor.  From there you can paste in this supplied override.conf file
Use Control-X to save.

Tell systemd to reload:

	systemctl daemon-reload

Restart the service
	
	systemctl restart <service>

Test it and look at its logs.
A first easy check:

	systemctl status

And look at the "State:" line.  It should say "State: running".

Look at:
	
	systemd-analyze security <service>

to see the improved score.

More info
https://unix.stackexchange.com/questions/398540/how-to-override-systemd-unit-file-settings

