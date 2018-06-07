# script.module.streamlink.base

You can install it from [repository.twilight0.libs](https://github.com/Twilight0/repo.twilight0.libs)

Add this to your repository xml in order to pull updates:

    <dir>
        <info compressed="false">http://raw.githubusercontent.com/Twilight0/repo.twilight0.libs/master/_zips/addons.xml</info>
        <checksum>http://raw.githubusercontent.com/Twilight0/repo.twilight0.libs/master/_zips/addons.xml.md5</checksum>
        <datadir zip="true">http://raw.githubusercontent.com/Twilight0/repo.twilight0.libs/master/_zips/</datadir>
    </dir>

## Extracting streams
### The simplest use of the Streamlink API looks like this:

    import streamlink
    streams = streamlink.streams("https://www.youtube.com/watch?v=XIMLoLxmTDw")
    try:
        url = streams.['best'].url
    except AttributeError:
        url = streams.['best'].to_url()  # You can get DASH streams' urls this way

Where url can be passed into the player:

    xbmc.Player().play(url)


If no plugin for the URL is found, a **NoPluginError** will be raised.

If an error occurs while fetching streams, a **PluginError** will be raised.

### Session based usage, which allows plugin options to be passed

    import streamlink.session

    def resolve(url, quality='best'):

        try:

            session = streamlink.session.Streamlink()
            # session.set_option("rtmp-rtmpdump", "/path/to/rtmpdump")
            plugin = session.resolve_url(url)
            streams = plugin.get_streams()
            try:
                playable_link = streams.[quality].url
            except AttributeError:
                playable_link = streams.[quality].to_url()

            return playable_link

        except:

            pass
