# script.module.streamlink.base

Default Streamlink Library for Kodi Addon [Twilight0/service.streamlink.proxy](https://github.com/Twilight0/service.streamlink.proxy)

You can install it from [repository.twilight0.libs](https://github.com/Twilight0/repo.twilight0.libs)

Sample code to use in your plugin & start using with the following snippet:

    import streamlink.session
    # import sys

    def resolve(url, quality='best'):

        try:

            session = streamlink.session.Streamlink()
            # session.set_loglevel("debug")
            # session.set_logoutput(sys.stdout)
            plugin = session.resolve_url(url)
            streams = plugin.get_streams()
            streams = repr(streams[quality])
            link = streams.partition('(\'')[2][:-3]

            return link

        except:
            pass
