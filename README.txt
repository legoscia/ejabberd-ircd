This is an IRC server frontend to ejabberd.  It supports a subset of
the IRC protocol, allowing IRC users to use a subset of Jabber MUC
functions.  Users log in with their username and password, just as if
they were Jabber users.  Therefore, configuring the IRC interface to
use an anonymous authentication backend is probably what users expect.
Channel names are translated to MUC rooms on a particular MUC service.

The most obvious missing functions in this module are operator actions
and a command to list channels.

Note that this module changes ejabberd_sup.erl, which may collide with
other extensions.  Merging the changes by hand should not be
difficult.

Something like this should be inserted in the "listen" section of the
configuration file:

  {6667, ejabberd_ircd,    [{access, c2s},
			    {host, "localhost"},
			    {muc_host, "conference.localhost"},
			    {encoding, "utf-8"},
			    {mappings,
			    [{"#esperanto", "esperanto@conference.jabber.org"}]}]},

access is the ACL matching users allowed to use the IRC backend.
host is the hostname part of the JIDs of IRC users.
muc_host is the MUC service hosting IRC "channels".
encoding is the encoding that IRC users are expected to use.
mappings is a list of mappings from channel names to MUC rooms on
other MUC services.

Author: Magnus Henoch, xmpp:legoscia@jabber.cd.chalmers.se,
mailto:henoch@dtek.chalmers.se
